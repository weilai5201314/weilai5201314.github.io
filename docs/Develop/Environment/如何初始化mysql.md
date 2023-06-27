# 如何初始化mysql

> 适用版本：mysql 8.x.x

1.下载mysql压缩包，解压 (选择你的焊胃者版本)

<https://downloads.mysql.com/archives/community/>

2.用**管理员身份**，切记是管理员身份打开命令行，进入mysql文件夹。

3.初始化 MySQL 数据目录：在命令行中，进入 MySQL 的bin目录，运行以下命令来初始化 MySQL 的数据目录（此命令创建的数据库`没有`密码，因此请连贯运行后续步骤）：

```shell
mysqld --initialize-insecure
```

4.安装 MySQL 服务：在命令行中，继续运行以下命令来安装 MySQL 服务：

```shell
mysqld --install
```

5.启动 MySQL 服务：在命令行中，运行以下命令来启动 MySQL 服务：

```shell
net start mysql
```

6.登录mysql，并且`修改`密码，此时mysql并没有密码，直接按`Enter`输入密码：

```mysql
mysql -u root -p
ALTER USER 'root'@'localhost' IDENTIFIED BY 'new_password';

#退出mysql
quit;

#可选步骤，再次登陆mysql，并输入你刚设置的密码
mysql -u root -p

```
