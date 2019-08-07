### Mysql 登录提示"ERROR 1045 (28000): Access denied for user 'root'@'localhost' (using password: YES)"

使用mysql -uroot -p,然后输入密码登录mysql时，出现了如下错误：

ERROR 1045 (28000): Access denied for user 'root'@'localhost' (using password: YES)

一般这个错误是由密码错误引起，解决的办法自然就是重置密码

解决方案如下：

1.停止mysql数据库：Mac在系统偏好设置里手动停止

2.用以下命令启动MySQL，以不检查权限的方式启动：

mysqld --skip-grant-tables &

3.登录mysql：mysql -u root -p

4.更新root密码

mysql的版本为5.7.20，以下命令在MySQL命令行里输入

UPDATE mysql.user SET authentication_string=PASSWORD('123456') where USER='root';

5.刷新权限：flush privileges;

6.退出mysql命令行：使用ctrl+D

7.使用root用户重新登录mysql

mysql -u root -p

Enter password:<输入新设的密码123456>

