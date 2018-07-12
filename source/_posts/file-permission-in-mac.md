title: Mac下文件权限查看与设置
date: 2018-07-01 19:39:36
categories: javascript
---

介绍Unix、Linux下文件和权限。

<!-- more -->



## 举例



```bash
# 我们先创建一个测试目录
$ mkdir test && cd test
# 创建一个main.txt文件并写入一些内容
$ echo hello world >> text.txt
# 再创建一个空目录
$ mkdir js
# 查看信息
$ ls -l
total 8
drwxr-xr-x  2 frank  staff  64  7 12 20:03 js # 这行就是js目录的信息
-rw-r--r--  1 frank  staff  13  7 12 19:52 main.txt # 这行是main.txt的信息
```

如上所示，文件和目录都具有如下信息：
```bash
# 权限信息通用格式：
-rwxr-xr-x　number　user　group　filesize　updatetime　filename
```

通用格式共分成7部分，分别是：

1. 文件属性，表示文件的类型是读/写/可执行等权限，共10个字符；
   - 第一个字符表示类型，后面9个字符分3组，表示该文件相对于当前用户(user)、当前用户所在的组(group)和其他用户(other)的读/写/可执行权限。
   - rwx：代表权限，-代表无权限，r代表read具有可读权限；w代表write具有可写权限；x代表execute具有可执行权限
   - 拿上面的`main.txt`举例，第一个字符是-，表示是文件类型；而`js`目录第一个字符是`d`，表示`directory`目录
   - 接下来的3个字符是`rw-，`表示该文件对于当前用户的权限是可读可写，但是不能执行
   - 再接下来的3个字符是`r--`，表示该文件对于当前用户所在的组的成员来说，只有只读权限，写和可执行都是没有权限的
   - 最后的3个字符也是`r--`，表示该文件对于其他用户来说也是只能读，不能写和执行
2. number,表示文件inode数量，inode表示存储文件原信息的区域；
3. user, 表示当前用户名
4. group， 表示当前用户所在的用户组的名字
5. filesize，表示文件的大小，单位是byte
6. updatetime，表示文件的最后修改时间
7. filename，表示文件名



## 修改文件权限

`main.txt`的权限是`-rw-r--r--  1 frank  staff  13  7 12 19:52 main.txt`，对其他用户的权限是`r--`，即只能读不能写，如果有个需求想让其他用户可写怎么办？这时候就需要修改`main.txt`的权限了，让其他用户也能进行写操作。



```bash
# 修改权限的命令格式
$ [sudo] chmod [<权限范围><权限操作><具体权限>] [文件或目录]
```



1. 权限范围
   - u: user，表示文件或目录的拥有者
   - g: group，表示文件或目录所属的组
   - o: other，除了文件或目录拥有者或者所属组之外的，其他用户都属于这个范围
   - a: all，即全部用户，包含文件或目录的拥有者、所属群组和其他用户
2. 权限操作
   - `+`表示增加权限
   - `-`表示取消权限
   - `=`表示唯一设定权限
3. 具体权限
   - `r`表示可读取
   - `w`表示可写入
   - `x`表示可执行



解释了这么多，现在我们通过命令操作，让`其他用户`对`main.txt`也有写的权限：

```bash
# 让其他用户具有写权限
$ chmod o+w main.txt
# 确认
$ ls -l main.txt
-rw-r--rw-  1 frank  staff  13  7 12 19:52 main.txt

# 让所有用户具有可执行权限，但是不可以修改且不可读
$ chmod a+x-r-w main.txt
# 再次确认
---x--x--x  1 frank  staff  13  7 12 19:52 main.txt
```

