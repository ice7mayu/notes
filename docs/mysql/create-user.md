# Create new user

```sql
$ mysql -u root -p
> # enter password

mysql> CREATE USER 'export'@'%' IDENTIFIED BY '123456';
mysql> GRANT ALL PRIVILEGES ON bitnami_testlink.* TO 'export'@'%';
mysql> FLUSH PRIVILEGES;
mysql> quit
```
