# Mysql

## login
```
mysql -uroot -h 127.0.0.1 -P 3306 -ppassword
```

## 导出数据库表
```sql
mysqldump -uroot -ppassword --databases db1 --tables a1 a2 >/tmp/db1.sql
```