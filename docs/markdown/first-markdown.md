# VSCode编写MarkDown文档

## VScode

VScode是一款免费开源的跨平台文本、代码编辑器。
VScode如何使用markdown编写文本？

1. Ctrl+Shift+P：打开控制命令行
2. 输入 install extensions，打开插件查询界面
3. 输入markdown，即可查找所有关于markdown的插件

## 使用markdown编辑文件

建立一个.md文件即可

## markdown常用命令

### 标题

```text
标题前加 #空格，如下所示
# 一级标题
## 二级标题
### 三级标题
#### 四级标题
##### 五级标题
```
  
### 字体

- 加粗

    在加粗的内容前后分别加上**或者__
    例如： **test**  __test__
- 斜体
  
    在斜体的内容前后分别加上*或者_
    例如： *test* _test_

- 斜体加粗
  
    在斜体加粗的内容前后分别加上***  
    例如： ***test***

- 删除线

    在需要删除的内容前后分别加上~~
    例如：~~test~~

### 引用

在引用的文字前加即可

例如：>test
多行引用在每行添加 > 即可

### 嵌套引用

例如：
>test parent
>>test children

第一行引用1个>
子引用中2个>，即>>

### 图片

![图片alt](图片地址 ''图片title'')

例如：
![test](https://ss0.bdstatic.com/94oJfD_bAAcT8t7mm9GUKT-xh_/timg?image&quality=100&size=b4000_4000&sec=1578935381&di=84833e1348beeab938026b237a834ccb&src=http://hiphotos.baidu.com/aphroditehitler/pic/item/c84ecd5c8fee9777faf2c014.jpg "海贼王")

### 超链接

[超链接名](超链接地址 "超链接title")

例如：
[百度](http://baidu.com "baidu")

[![test](https://ss0.bdstatic.com/94oJfD_bAAcT8t7mm9GUKT-xh_/timg?image&quality=100&size=b4000_4000&sec=1578935381&di=84833e1348beeab938026b237a834ccb&src=http://hiphotos.baidu.com/aphroditehitler/pic/item/c84ecd5c8fee9777faf2c014.jpg "海贼王")](http://baidu.com "baidu")

### 列表

#### 无序列表

`-, + *` 加空格

例如：

```text
- test
+ test
* test
```
  
#### 有序列表

数字、字母加空格

例如：

1. test
2. test

#### 列表嵌套

上一级和下一级之间敲三个空格即可

例如：

- testOne
  
  - testTwo
  
  - testThree
  
#### 代码

- 一行代码
  
使用1个 `` ` ``, 例如：

`print(Hello world!)`

- 代码块
  
使用3个 `` ``` ``, 例如：

```java
String i = "test";
print(i)
```
