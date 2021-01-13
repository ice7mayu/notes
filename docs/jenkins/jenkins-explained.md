# Jenkins

## What is Jenkins

Jenkins 是一个任务调度工具, 能够定制流程类的 Job 作业, 并提供统一的中心管理界面或API, 对作业进行配置.

## How does it work

![jenkins-overview-feature-overview](images/jenkins-overview-feature-overview.svg)

![jenkins-overview-explain-workflow](images/jenkins-overview-explain-workflow.svg)

## Installation and Configurations

Jenkins 提供以下两种安装部署方式:

- 下载安装包, 包含 Jenkins 应用和 Web服务器.
- 下载 .war 包, 需要自行搭建 Java Web 服务器, 例如 tomcat 然后部署 jenkins.war.

### Plugins

Jenkins 的能力来源于各种插件, 通过安装所需的插件来满足对功能的需求.

- Groovy: 通过执行 groovy 脚本对 Jenkins 进行系统设置, 例如(CSP).
- Startup Trigger: 重启 Jenkins 服务时, 自动触发执行任务.
- File Operations: 对文件进行操作, 新建文件, 复制文件等.
- Multiple SCMs plugin: 管理多个 Git 代码库.
- HTML Publisher plugin: 显示 html report.
- JUnit Plugin: 显示 JUnit 格式测试结果.
- Allure Jenkins Plugin: 生成并展示 Allure 报告.
- Role-based Authorization Strategy: 基于角色及任务的认证管理.(本地安装时为可选)

### Slave Machines

用于承载 Jenkins 应用的机器叫做 Master, 可以直接用来执行 Job.
在 Jenkins 中也可以添加配置一些 Slave 执行机, 来执行 Job.
Master 和 Slave 之间以标准的协议通信, 适用于全平台(Linux, MacOS, Windows),
所以 Slave 为 Jenkins 提供了跨平台的执行能力.

Slave 相关软件:

- RDCMan: 用于远程连接并登录执行机.
- VNC: 通过网络协议远程连接并登录执行, 可能使 Windows 系统一直保持登录状态, 进行桌面应用自动化.

### Run Job

- Live Demo

----
Done
