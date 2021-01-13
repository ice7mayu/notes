# Update Center

During the installation process and hit below error:

```log
2019-11-05 02:01:43.970+0000 [id=40]    INFO    hudson.util.Retrier#start: The attempt #1 to do the action check updates server failed with an allowed exception:
java.net.SocketTimeoutException: connect timed out
        at java.net.PlainSocketImpl.socketConnect(Native Method)
        at java.net.AbstractPlainSocketImpl.doConnect(AbstractPlainSocketImpl.java:350)
        at java.net.AbstractPlainSocketImpl.connectToAddress(AbstractPlainSocketImpl.java:206)
        at java.net.AbstractPlainSocketImpl.connect(AbstractPlainSocketImpl.java:188)
        at java.net.SocksSocketImpl.connect(SocksSocketImpl.java:392)
2019-11-05 02:01:43.971+0000 [id=40]    INFO    hudson.util.Retrier#start: Calling the listener of the allowed exception 'connect timed out' at the attempt #1 to do the action check updates server
2019-11-05 02:01:43.977+0000 [id=40]    INFO    hudson.util.Retrier#start: Attempted the action check updates server for 1 time(s) with no success
2019-11-05 02:01:43.985+0000 [id=27]    WARNING hudson.model.UpdateCenter#updateDefaultSite: Upgrading Jenkins. Failed to update the default Update Site 'default'. Plugin upgrades may fail.
java.net.SocketTimeoutException: connect timed out
        at java.net.PlainSocketImpl.socketConnect(Native Method)
        at java.net.AbstractPlainSocketImpl.doConnect(AbstractPlainSocketImpl.java:350)
        at java.net.AbstractPlainSocketImpl.connectToAddress(AbstractPlainSocketImpl.java:206)
        at java.net.AbstractPlainSocketImpl.connect(AbstractPlainSocketImpl.java:188)
2019-11-05 02:01:44.018+0000 [id=40]    SEVERE  hudson.PluginManager#doCheckUpdatesServer: Error checking update sites for 1 attempt(s). Last exception was: SocketTimeoutException: connect timed out
2019-11-05 02:01:44.058+0000 [id=40]    INFO    hudson.model.AsyncPeriodicWork$1#run: Finished Download metadata. 36,249 ms
2019-11-05 02:01:44.078+0000 [id=27]    INFO    jenkins.InitReactorRunner$1#onAttained: Completed initialization
```

This is due to Jenkins can't connect to the update server through HTTPS connections:

```log
2019-11-05 02:01:43.985+0000 [id=27]    WARNING hudson.model.UpdateCenter#updateDefaultSite: Upgrading Jenkins. Failed to update the default Update Site 'default'. Plugin upgrades may fail.
java.net.SocketTimeoutException: connect timed out
```

Locate and edit the config file *$JENKINS_HOME/hudson.model.UpdateCenter.xml*

```xml
<?xml version='1.1' encoding='UTF-8'?>
<sites>
  <site>
    <id>default</id>
    <url>https://updates.jenkins.io/update-center.json</url>
  </site>
```

Use the HTTP connection:

```text
http://updates.jenkins.io/update-center.json
```

or check mirrors at <http://mirrors.jenkins-ci.org/status.html>

Find one and change update url to:

```text
https://mirrors.tuna.tsinghua.edu.cn/jenkins/updates/update-center.json
```
