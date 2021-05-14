---
 title: mysql授权远程登录 
 date: 2021/03/23 10:01:16 
 tags: 
 - blog 
---

### mysql授权远程登录

```mysql
mysql -uroot -p # 进入mysql
use mysql # 进入mysql数据库
select host, user from user; # 查看现在允许访问的用户以及对应的host
# 添加新的授权
grant all privileges on *.* to '用户名'@'ip[% 代表所有来源]' identified by '登录密码' with grant option;
# 案例：
# 给用户test一个abc123的密码，授权给192.168.1.100的用户使用
# grant all privileges on *.* to 'test'@'192.168.1.100' identified by 'abc123' with grant option;
flush privileges; # 重要，添加完授权后要刷新权限
```

