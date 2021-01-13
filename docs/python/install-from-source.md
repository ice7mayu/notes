# How to Install Python 3.7 from source on CentOS

Original Posts.

- <https://tecadmin.net/install-python-3-7-on-centos/>
- <https://joshspicer.com/python37-ssl-issue>
- <https://computingforgeeks.com/how-to-install-python-on-3-on-centos/>

## Install or upgrade system requiremnts before installing

```bash
yum install gcc openssl-devel bzip2-devel libffi-devel
```

## Download and extract Python 3.7

```bash
$ cd ~/download
wget https://www.python.org/ftp/python/3.7.3/Python-3.7.3.tgz

tar xzvf Python-3.7.3.tgz
```

## Install from source

```bash
cd Python-3.7.3
./configure --enable-optimizations
make altinstall
```

`make altinstall` is used to prevent replacing the default python binary file `/usr/bin/python`. Your installation will be `/usr/local/bin/python3.7`.

## Check Python version

Make sure your installation not replacing the system python.

```bash
$ which python
/usr/bin/python

$ which python3.7
/usr/local/bin/python3.7
```

## Check if pip works fine

```bash
pip list
# or
pip install <package>
```

## Reinstall OpenSSL and re-compile Python source

If you hit below error when you pip install some modules.

```text
pip is configured with locations that require TLS/SSL, however the ssl module in Python is not available.

    Retrying (Retry(total=1, connect=None, read=None, redirect=None, status=None)) after connection broken by 'SSLError("Can't connect to HTTPS URL because the SSL module is not available.")'
```

Then you have to install OpenSSL and re-configure ssl location before compiling Python source.

To install OpenSSL.

```bash
cd ~/download
wget https://www.openssl.org/source/openssl-1.0.2q.tar.gz
tar xvf openssl-1.0.2q.tar.gz
cd openssl-1.0.2q
./config
make && make install
```

Now newly installed ssl will be located at `/usr/local/ssl`.

Download and extract Python3.7

```bash
$ cd ~/download
wget https://www.python.org/ftp/python/3.7.3/Python-3.7.3.tgz

tar xzvf Python-3.7.3.tgz
```

Go to the extracted folder and edit `Modules/Setup.dist`

```bash
cd Python-3.7.3
vim Modules/Setup.dist
```

Uncomment these SSL lines to tell python where to find `ssl`.

```text
# Socket module helper for SSL support; you must comment out the other
# socket line above, and possibly edit the SSL variable:
:SSL=/usr/local/ssl
 _ssl _ssl.c \
    -DUSE_SSL -I$(SSL)/include -I$(SSL)/include/openssl \
    -L$(SSL)/lib -lssl -lcrypto
```

Now you can finish up the installation scripts.

```bash
./configure --enable-optimizations
make altinstall
```

At this point you will have a working python and pip (mapped to python3.7 and pip3.7 in your path).