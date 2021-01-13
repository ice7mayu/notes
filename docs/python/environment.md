# 搭建本地环境

## 1.下载PyCharm

目前使用最新的
[pycharm2019](https://www.jetbrains.com/pycharm/download/#section=windows)，
安装pycharm成功后，配置python解释器

## 2.安装解释器

目前使用的解释器是3.8版本

- 下载python解释器
[python-3.8](https://www.python.org)，并安装
- 配置环境变量
 E:\Python\python-38;
 E:\Python\python-38\Scripts;

## 3.下载代码

从git上下载项目代码

## 4.配置venv虚拟环境

在项目的目录下创建一个子目录.venv来存放虚拟环境

```python
python -m venv  .venv
```

虚拟环境创建成功，检查目录结构

 ![.venv目录结构](https://img-blog.csdnimg.cn/20200108220824424.png)

启动虚拟环境

```batch
.venv\Scripts\activate.bat
```

虚拟环境启动成功后，会启动一个子界面，在命令行提示符前显示当前虚拟环境的名称（.venv）
![.venv启动成功后](https://img-blog.csdnimg.cn/20200108221105890.png)

关闭虚拟环境

```batch
deactivate
```

关闭虚拟环境后就退出到系统级环境

## 5.使用requirements.txt文件管理依赖

在python中需要依赖的外部模块可以管理到requirements.txt文件中，方便在新的系统上部署时使用。

创建requirements.txt文件，进入到项目的根目录下，执行命令：

```batch
pip freeze > requirements.txt
```

## 6.使用pip安装类库

python的环境类库是根据项目隔离的，因此每个项目需要下载自己的类库。

```batch
pip install -r requirements.txt
```

![使用pip下载类库](https://img-blog.csdnimg.cn/20200108222456405.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3UwMTExMzMwMDc=,size_16,color_FFFFFF,t_70)

查看安装的类库

```batch
pip list
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/2020010913131623.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3UwMTExMzMwMDc=,size_16,color_FFFFFF,t_70)

以上，python环境搭建完成。
