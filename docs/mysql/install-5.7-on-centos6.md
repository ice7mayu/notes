# Install mysql 5.7 on CentOS6.6

## Prep ENV

Install `cmake`:

```bash
yum install cmake
```

Install `libnuma`:

```bash
yum install numactl
```

Remove mysql-lib

```bash
yum remove mysql-libs
```

## Install MySQL

Download RPM bundle then unpack:

<https://downloads.mysql.com/archives/community>

```bash
tar -xvf mysql-5.7.21-1.el6.x86_64.rpm-bundle.tar
```

Install server & client

```bash
yum install mysql-community-server-5.7.21-1.el6.x86_64.rpm
yum install mysql-community-client-5.7.21-1.el6.x86_64.rpm
```

## Change root password

Find the initial password.

```bash
cat /var/log/mysqld.log
cat /root/.mysql_secret
```

```text
2020-12-17T03:50:50.533236Z 1 [Note] A temporary password is generated for root@localhost: waYH5h?9<b_h
```

Login in as root with initial password:

```bash
$ mysql -u root -p
Enter password:
```

Set a new password for the current root user:

```bash
mysql> set password=PASSWORD('ql3.Admin');
```

## Create user

Create a new user:

```sql
>mysql create user 'ql3db'@'%' identified by 'ql3DB@jd.com';
>mysql GRANT ALL PRIVILEGES ON *.* TO 'ql3db'@'%';
>mysql FLUSH PRIVILEGES;
>mysql quit
```
