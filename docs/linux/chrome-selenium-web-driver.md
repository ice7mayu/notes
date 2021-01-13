# Setup Google Chrome and Selenium Webdriver on CentOS 7

## Useful Links

[Running Selenium Headless with Chrome](https://linuxhint.com/chrome_selenium_headless_running/)

## Install Google Chrome

Add Chrome official yum repo:

```bash
cat /etc/yum.repos.d/google-chrome.repo
```

```yum
[google-chrome]
name=google-chrome
baseurl=http://dl.google.com/linux/chrome/rpm/stable/x86_64
enabled=1
gpgcheck=1
gpgkey=https://dl.google.com/linux/linux_signing_key.pub
```

Install chrome with yum:

```bash
yum install google-chrome-stable
```

By using Google’s official repository you will keep your Chrome browser up-to-date.

```bash
yum update google-chrome-stable
```

## Download Chrome Webdriver

To download Chrome Web Driver, visit the [official Chrome Driver download page.](https://chromedriver.chromium.org/downloads)

Unzip chromedriver:

```bash
unzip ~/chromedriver_linux64.zip -d drivers/
```

## Run webdriver in headless mode

```python
options = Options()
options.add_argument("--headless")
options.add_argument("--no-sandbox")
options.add_argument("--disable-gpu")

driver = webdriver.Chrome(executable_path="/path/to/chromedriver", options=options)
```
