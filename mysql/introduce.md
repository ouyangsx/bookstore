# mysql简介
<!-- toc -->

### 数据库

1. 数据库的好处：

   + 持久化数据到本地；
   + 可以实现结构化查询，方便管理

2. 数据库的相关概念：

   + DB：

     数据库（database），存储数据的仓库，保存了一系列有组织的数据。

   + DBMS：

     数据库管理系统（Database Management System），数据库是通过DBMS创建和操作的容器。

   + SQL：

     结构化查询语言（Structure Query Language），专门用来与数据库通信的语言。

3. 数据库的特点：

   + 将数据放到表中，再将表放到库中；
   + 一个数据库中可以有多张表，每个表都有一个唯一的名字来标识自己；
   + 表具有一些特性，这些特性定义了数据在表中如何存储，类似于Java中“类”的设计；
   + 表由列组成，也成为字段，所有表都是由一个或多个列组成的，每一列类似Java中的属性；
   + 表中的数据是按照行存储的，每一行类似于Java中的对象。

### MySql

1. DBMS的种类：

   基于共享文件系统的DBMS(Acess)；

   基于客户机-服务器的DBMS（MySql、Oracle、SQL server）

2. MySQL的安装和卸载：

   MySQL是C/S结构，底层是TCP/IP协议的程序，在服务器端，先启动，有一个端口号，监听/支持客户端的连接。

   + 卸载：
     + 先停止MySQL服务；
     + 卸载MySQL软件；
     + 删除残留文件，删除注册表；

3. MySQL服务的启动和停止：

   以管理员身份打开命令提示符：

   ```mysql
   #启动MySQL服务：
   net start mysql
   #停止MySQL服务：
   net stop mysql
   ```

4. MySQL服务端的登录和退出：

   ```mysql
   #登录：
   mysql (-h主机名 -P端口号) -u用户名 -p密码
   #退出：
   exit
   ```

5. 查看MySQL服务器版本：

   ```mysql
   mysql --version
   ```

6. MySQL常见命令：

   ```mysql
   #查看当前所有的数据库：
   show databases;
   #打开指定的库：
   use 库名;
   #查看当前库的所有表：
   show tables;
   #查看其他库的所有表：
   show tables from 库名;
   #创建表：
   create table 表名(
   	列名 数据类型，
       列名 数据类型，
       ....
   );
   #查看当前所在的库：
   select databases();
   #查看表结构：
   desc 表名;
   ```

7. MySQL语法规范：

   + 不区分大小写，但建议关键字大写，表名、列名小写；

   + 每条命令最好用分号结尾；

   + 每条命令根据需要，可以进行缩进或者换行；

   + 注释：

     单行注释：#注释文字

     单行注释：--   注释文字

     多行注释：/\* 注释文字 \*/
   
8. sql语言的分类：

   + DDL(Data Definition Language)：数据定义语言，用来定义数据库对象：库、表、列等；create/drop/alter
   + DML(Data Manipulation Language)：数据操作语言，用来定义数据库记录（数据）；insert/update/delete
   + DCL(Data Control Language )：数据控制语言，用来定义访问权限和安全级别；
   + DQL(Data Query Language)：数据查询语言，用来查询记录（数据）;select

