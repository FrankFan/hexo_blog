title: Oracle常用存储过程写法
date: 2014-04-04 23:46:22
categories: database
---
## 写在前面
这段时间工作最长接触到的就是Oracle数据库，不论查数据，还是统计、运行job，都离不开PL/SQL 存储过程，下面就整理下经常用到的知识。

## 一、Function函数
函数是执行非查询语句的方法。

* 创建返回list的function

```sql
CREATE OR REPLACE FUNCTION FNTOPWEEKESLIST (
   ininttype       IN       INTEGER,
   outcurlist      OUT      pkgrefcursor.refcursor
)
   RETURN INTEGER
IS
Begin
   OPEN outcurlist FOR
    SELECT t.all, a.bookname
    FROM tbbookestimatestats t, tbbook a
    WHERE t.intype = ininttype
    and t.bookid = a.bookid
    and a.freetype = 0;
   RETURN 0;
END;
```


* 创建带分页的返回list的function


```sql
CREATE OR REPLACE FUNCTION fn_source_pay_getlist(indtbegin       DATE,
                                                 indtend         DATE,
                                                 invarsourcename VARCHAR2,
                                                 inintpagesize   IN INTEGER,
                                                 inintpageindex  IN INTEGER,
                                                 outintRowCount  out integer,
                                                 outcurlist      OUT pkg_refcursor.ref_cursor)
  RETURN INTEGER 
  as
begin
  select count(1)
    into outintRowCount
    from tbcl_resu_payuser
   where source = case
           when length(invarsourcename) > 0 then
            invarsourcename
           else
            source
         end
     and trunc(datetime) >= indtbegin
     and trunc(datetime) < indtend;
  open outcurlist for
    select *
      from (select a.*, row_number() over(order by a.datetime) rn
              from (select source,
                           datetime,
                           payusercnt1,
                           payusercnt2,
                           payusercnt3,
                           payusercnt4
                      from tbcl_resu_payuser
                     where source = case
                             when length(invarsourcename) > 0 then
                              invarsourcename
                             else
                              source
                           end
                       and trunc(datetime) >= indtbegin
                       and trunc(datetime) < indtend
                     order by datetime) a)
     where rn between inintpagesize * (inintpageindex - 1) + 1 and
           inintpagesize * inintpageindex;
  return 0;
end;
```

* 返回普通值的function


```sql
CREATE OR REPLACE FUNCTION FNACTIVEDAYSUSECNTGET (inintactivetype INTEGER,
						inintuserid     integer,
						outintgetcnt   out integer,--总抽奖次数 
						outintusercnt  out integer)--用户抽奖次数
   RETURN INTEGER
IS
   -- 获取活动当天领取次数
   vcnt   INTEGER;
BEGIN
   SELECT NVL (MAX (cnt), 0)
     INTO outintgetcnt
     FROM tbactivestats
    WHERE logtime = TRUNC (SYSDATE) AND activetype = inintactivetype;    
   SELECT count(1)
     INTO outintusercnt
     FROM tbuseractivegiftlog
    WHERE userid = inintuserid AND activetype = inintactivetype;    
   RETURN 0;
END;
```

或者这样:

```sql
CREATE OR REPLACE FUNCTION FNUSERCOSTGET(invarptid   IN varchar2,
                                           inintbookid in integer)
  RETURN integer 
  IS
  vamount integer;
BEGIN
  select nvl(max(amount), 0)
    into vamount
    from tbuserbookcost
   where ptid = lower(invarptid)
     and bookid = inintbookid;
  return(vamount);
EXCEPTION
  WHEN others THEN
    return(0);
END;
```

## 二、Procedure过程

* 更新update

```sql
CREATE OR REPLACE PROCEDURE "ADDUPDATEBOOKLOG" (inintbookid   IN  INTEGER,
						inintfreetype IN  INTEGER,
						outintresult  OUT INTEGER) AS
/*
  功能：插入一条记录
  传入参数：bookid，freetype
  输出参数：是否插入成功
*/
BEGIN
      如果存在就更新记录
     UPDATE tbupdatebooklog
     SET createtime = SYSDATE, freetype = inintfreetype
     WHERE bookid = inintbookid;
     --如果不存在就插入记录
     IF SQL%ROWCOUNT = 0 THEN
        INSERT INTO tbupdatebooklog(bookid, createtime, freetype)
        VALUES(inintbookid, SYSDATE, inintfreetype);
     END IF;
     COMMIT;
     outintresult := 0;
EXCEPTION
     WHEN OTHERS THEN
     outintresult := 1;
     ROLLBACK;
END AddUPdateBookLog;
```

或者：

```sql
CREATE OR REPLACE PROCEDURE PRBOOKSIGNSTATUSSET(inintBookId     integer,
                                                  invarSignStatus varchar2,
                                                  outintresult    out integer) is

begin
  update tbbook t
     set t\.signstatus = invarSignStatus
   where bookId = inintBookId;
  commit;
  outintresult := 0;
end prbookSignStatusset;
```

* 插入insert


```sql
CREATE OR REPLACE PROCEDURE "PRBOOKTYPEUPDLOGINS" (
   inintbookid              IN       INTEGER,
   ininttypeid        		IN       INTEGER,
   invatypename      		IN       varchar2,
   outintresult             OUT      INTEGER
)
IS
   vcnt   INTEGER;
BEGIN
   insert into tbbooktypeupdlog(bookid,updatetime,typeid,typename)
   values (inintbookid,sysdate,ininttypeid,invartypename);
   commit;
   outintresult:=0;
END;
```

## 三、Package包
包是有包头和包体组成的一组具有共性的函数或者过程。

1.声明包

```sql
CREATE OR REPLACE PACKAGE PKGTEST is
    TYPE refcursor IS REF CURSOR;
    procedure add();
    procedure update();
    procedure get();
end pkgTEST;
```
 
2.定义包体

```sql
CREATE OR REPLACE PACKAGE BODY PKGTEST is
    TYPE refcursor IS REF CURSOR;
    procedure add() IS 
    BEGIN
      ...
    END;
    procedure update() IS
    BEGIN
      ...
    END;
    procedure get() IS
    BEGIN
      ...
    END;
end pkgTEST;
```