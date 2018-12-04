下载：[官网下载](https://dev.mysql.com/downloads/mysql/)

配置 my.ini 文件

```
[mysql]
# 设置mysql客户端默认字符集
default-character-set=utf8
 
[mysqld]
# 设置3306端口
port = 3306
# 设置mysql的安装目录
basedir=C:\\web\\mysql-8.0.11
# 设置 mysql数据库的数据的存放目录，MySQL 8+ 不需要以下配置，系统自己生成即可，否则有可能报错
# datadir=C:\\web\\sqldata
# 允许最大连接数
max_connections=20
# 服务端使用的字符集默认为8比特编码的latin1字符集
character-set-server=utf8
# 创建新表时将使用的默认存储引擎
default-storage-engine=INNODB
```

初始化数据库

以管理员身份打开 cmd 命令行工具进入目录。直接在当前目录使用 powershell 会报错。

```
cd D:\mysql-8.0.13-winx64
```

初始化

```
mysqld --initialize --console
```

输出有一条这样的记录

```
2018-12-04T02:27:09.298372Z 5 [Note] [MY-010454] [Server] A temporary password is generated for root@localhost: oEYylKCsX4)Q
```

这是默认密码，一定要保存下来

安装

```
mysqld install
```

启动
```
net start mysql
```

登陆

```
mysql -u root -p
```

回车后要求输入密码，输入刚才保存的密码 `oEYylKCsX4)Q`。登陆成功会提示 `Welecome to the MySQL ...` 表示登陆成功。


[菜鸟教程 - mysql教程](http://www.runoob.com/mysql/mysql-install.html)