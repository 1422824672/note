### Linux操作系统常用命令

#### 	文件基本属性

- 显示文件的属性以及文件所属的用户和组

```shell
ls -l

[root@VM-20-11-centos ~]# ls -l
total 44
-rw-r--r-- 1 root root  1781 Apr  8  2021 cosfs.sh
-rw-r--r-- 1 root root  1237 Jan 28  2021 dnspod.sh
-rw-r--r-- 1 root root 25166 Jan 14 11:27 install_panel.sh
-rw-r--r-- 1 root root  2258 Mar  3  2021 install.sh
-rw-r--r-- 1 root root  1219 Feb  5  2021 txcdn.sh

```

- 更改文件属组

```shell
chgrp [-R] 属组名 文件名
```

- 更改文件属主，也可以同时更改文件属组

```shell
chown [–R] 属主名 文件名
chown [-R] 属主名：属组名 文件名
```

- 每种身份的不同权限分数

```shell
r:4
w:2
x:1
```

- 利用权限分数变更文件权限

```shell
chmod 777 sys.log
```

#### 文件与目录管理

- 处理目录的常用命令

```shell
ls（英文全拼：list files）: 列出目录及文件名
cd（英文全拼：change directory）：切换目录
pwd（英文全拼：print work directory）：显示目前的目录
mkdir（英文全拼：make directory）：创建一个新的目录
rmdir（英文全拼：remove directory）：删除一个空的目录
cp（英文全拼：copy file）: 复制文件或目录
rm（英文全拼：remove）: 删除文件或目录
mv（英文全拼：move file）: 移动文件与目录，或修改文件与目录的名称
```

- ls（列出目录）

```shell
-a ：全部的文件，连同隐藏文件( 开头为 . 的文件) 一起列出来(常用)
-d ：仅列出目录本身，而不是列出目录内的文件数据(常用)
-l ：长数据串列出，包含文件的属性与权限等等数据；(常用)

[root@www ~]# ls -adl ~
[root@www ~]# ls -l ~
```

- cd （切换目录）

```shell
#使用 mkdir 命令创建 baiqingyang 目录
[root@www ~] mkdir baiqingyang
#使用绝对路径切换到 baiqingyang 目录
[root@www ~] cd /root/baiqingyang/
#使用相对路径切换到 baiqingyang 目录
[root@www ~] cd ./baiqingyang/
# 表示回到自己的家目录，亦即是 /root 这个目录
[root@www runoob] cd ~
# 表示去到目前的上一级目录，亦即是 /root 的上一级目录的意思；
[root@www ~] cd ..
```

- pwd （显示目前所在目录）

```shell
[root@www ~]# pwd
/root   <--当前所在目录
```

- mkdir（创建新目录）

```shell
[root@www ~]# mkdir [-mp] 文件名称
-p 如果不使用-p属性时，创建未存在路径目录会报错，使用此参数可以直接将创建路径上未创建的目录创建出来
-m 在创建目录的同时配置权限
[root@www ~]# cd /tmp
[root@www tmp]# mkdir test    
[root@www tmp]# mkdir test1/test2/test3/test4 没用使用-p，test1 2 3没有被创建，会报错
[root@www tmp]# mkdir -p test1/test2/test3/test4 不会报错
[root@www tmp]# mkdir -m 711 test
[root@www tmp]# ls -l
drwxr-xr-x  3 root  root 4096 Jul 18 12:50 test
```

- rmdir（删除空的目录）

```shell
[root@www ~]# rmdir [-p] 文件名称
-p 会级联删除多级空目录
[root@VM-20-11-centos tmp]# rmdir -p test1/test2/test3/test4/
```

- cp（复制文件或目录）

```shell
[root@www ~]# cp [-air] 来源档(source) 目标档(destination)
-i：若目标档(destination)已经存在时，在覆盖时会先询问动作的进行
-r：递归持续复制，用於目录的复制行为
[root@VM-20-11-centos tmp]# mkdir ./test1
[root@VM-20-11-centos tmp]# cp -r ./test ./test1/
[root@VM-20-11-centos test1]# ls
test
```

- rm（移除文件或目录）

```shell
 rm [-fir] 文件或目录
 [root@www tmp]# rm -i bashrc
rm: remove regular file `bashrc'? y
```

- mv（移动文件与目录，或修改名称）

```shell
[root@www ~]# cd /tmp
[root@www tmp]# cp ~/.bashrc bashrc
[root@www tmp]# mkdir mvtest
[root@www tmp]# mv bashrc mvtest
```

- cat （由第一行开始显示文件内容）

```shell
[root@www ~]# cat /etc/issue
```

- tac （从最后一行开始显示文件内容，这是cat的倒写）

```shell
[root@www ~]# act /etc/issue
```

#### Linux用户和用户组管理常用命令

- useradd （添加新用户账号）

```shell
[root@www ~]# useradd –d  /home/xiaoming -m xiaoming
此命令创建了一个用户xiaoming，其中-d和-m选项用来为登录名xiaoming产生一个主目录 /home/xiaoming（/home为默认的用户主目录所在的父目录）
```

- userdel （删除账号）

```shell
[root@www ~]# userdel -r xiaoming
此命令创建了一个用户xiaoming，其中-d和-m选项用来为登录名xiaoming产生一个主目录 /home/xiaoming（/home为默认的用户主目录所在的父目录）
```

#### 
