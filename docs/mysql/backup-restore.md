# MySQL backup & restore

[Dumping Data in SQL Format with mysqldump][MySQL doc]

Backup `mydatabase` to current dir as `mydatabase.sql` file:

```bash
mysqldump -u root --password=<password> mydatabase > mydatabase.sql
```

Restore from dump file:

```bash
mysql -u root --password=<password> mydatabase < mydatabase.sql
```

[MySQL doc]: https://dev.mysql.com/doc/mysql-backup-excerpt/5.7/en/mysqldump-sql-format.html