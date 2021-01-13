# Jenkins

## 本地安装Jenkins

- 下载Jenkins jar包
- 运行Jenkins

```bash
java -jar jenkins.war --httpPort=8080
```

- 浏览器打开：<http://localhost:8080>

## master

master是Jenkins的服务器，Master提供web接口供Job和Slave调用。

## slave

创建代理时需要给代理在Jenkins上指定一个文件夹路径，这个文件夹对于master来说不必知道在哪里。代理不会存储任何重要的数据，所有job配置、创建日志存在master上。因此，可以使用一个临时的文件夹作为代理的根目录。这个文件夹不会随着代理重启而被删除，所以代理可以缓存数据，例如，安装工具、创建workspace的数据，这样就可以防止代理重启时需要重新下载源码code或者下载工具。
代理可以随机执行job，可以按照标签配置执行哪些job。
代理和master之间是通过ssh或jnlp协议连接在一起的，两种协议的特点如下：

1. ssh来说，我们一般用的服务器都是linux系统，当然最方便的就是通过ssh启动jenkins节点，但是这个有个前提的要求就是master和slave之前能进行ssh连接
2. jnlp（Java web start）连接方式有个好处就是不用master和slave之间进行ssh连接，只需要ping成功即可。并且如果slave的机器是windows的话，也是可以的这个其实是非常实用的，因为有时候，可能一些权限或者防火墙的原因，这master和slave真的不能够ssh连接，还有一些未知的原因无法ssh到slave节点都可以通过jnlp的方式进行连接。

## 创建任务

doing...
