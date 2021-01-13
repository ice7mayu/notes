# Change timezone on CentOS

Original Post: <https://chrisjean.com/change-timezone-in-centos/>

There are a series of time zone files located at `/usr/share/zoneinfo`. Select the appropriate named timezone for your location. The active timezone used on your system is in the `/etc/localtime` file.

Backup your original `/etc/localtime` file.

```bash
mv /etc/localtime /etc/localtime.bak
```

Find your time zone file and link to `/etc/localtime`.

```bash
ln -s /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
```

Run `date` to see if your time zone is correct.
