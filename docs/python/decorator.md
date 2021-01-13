# 装饰器

装饰器是python提供的一种强大的语法，可以快速扩展一个方法的功能。

## 方法可以赋值给一个变量

```python
def greet(name):
    return "hello," + name


greet_someone = greet
print(greet_someone("Alice"))

```

```text
hello,Alice
```

## 方法可以定义在其他方法中

```python
def greet(name):
    def get_message():
        return "hello "

    result = get_message() + name
    return result


print(greet("Alice"))

```

```text
hello Alice
```

## 方法可以作为入参传给其他方法

```python
def greet(name):
    return "Hello," + name


def call_function(func):
    other_name = "Johnny"
    return func(other_name)


print(call_function(greet))
```

```text
Hello,Johnny
```

## 方法可以作为方法的返回值

```python
def say_hello():
    def greet():
        return "Hello,Alice"

    return greet


greet = say_hello()
print(greet())
```

```text
Hello,Alice
```

## 内部方法只能访问闭包

这种模式在构建装饰器时会遇到

```python
def compose_greet_func(name):
    def get_message():
        return "Hello there," + name

    return get_message


greet = compose_greet_func("Johnny")
print(greet())
```

```text
Hello there,Johnny
```

## 装饰器的构成

装饰器仅仅是对现有方法的封装
下面的例子是把一个方法的输出字符串用 `<p>` 包括

```python
def get_text(name):
    return f"Hello,{name}"


def p_decorate(func):
    def func_wrapper(name):
        return "<p>{0}</p>".format(func(name))

    return func_wrapper


my_get_text = p_decorate(get_text)
print(my_get_text("Alice"))
```

```text
<p>Hello,Alice</p>
```

装饰器就像一个数学函数y=f(x)，函数x经过一些规则变换映射到函数y
对于装饰器来说，这个规则如下：

```python
def p_decorate(func):
    def func_wrapper(*args, **kwargs):
        return "<p>{}</p>".format(func(*args, **kwargs))
```

func方法表示x，*args和**kwargs表示func函数的任意多个位置参数和关键字参数
func_wrapper方法表示对func函数做的处理，即为f()
p_decorate()方法返回的值即为y

另外，func_wrapper方法的另一个作用就是传递func方法的参数

## python的装饰器语法

如上，构造完装饰器后，在需要使用装饰器的方法前面加装饰器标签即可，如下

```python
def p_decorate(func):
    def func_wrapper(name):
        return "<p>{0}</p>".format(func(name))

    return func_wrapper

@p_decorate
def get_text(name):
    return f"Hello,{name}"


print(get_text("nimo"))
```

```text
<p>Hello,nimo</p>
```

## 装饰器支持嵌套使用

```python
def div_decorate(func):
    def func_wrapper(name):
        return "<div>{0}</div>".format(func(name))

    return func_wrapper


def p_decorate(func):
    def func_wrapper(name):
        return "<p>{0}</p>".format(func(name))

    return func_wrapper


def strong_decorate(func):
    def func_wrapper(name):
        return "<strong>{0}</strong>".format(func(name))

    return func_wrapper


my_get_text = p_decorate(get_text)
print(my_get_text("Alice"))


@div_decorate
@p_decorate
@strong_decorate
def get_text(name):
    return f"Hello,{name}"


print(get_text("nimo"))
```

```text
<div><p><strong>Hello,nimo</strong></p></div>
```

## 装饰器方法也可以有参数

```python
def tag(tag_name1, tag_name2, tag_name3):
    def p_decorate(func):
        def func_wrapper(name):
            return "<{2}><{1}><{0}>{3}</{0}></{1}></{2}>".format(tag_name1, tag_name2, tag_name3, func(name))

        return func_wrapper

    return p_decorate


@tag("strong", "p", "div")
def get_text(name):
    return f"Hello,{name}"
```

```text
<div><p><strong>Hello,nimo</strong></p></div>
```

## Decorator execution order

- Execution order: outermost first
- Return order: innermost first

Example:

```python
def make_bold(fn):
    def wrapper():
        print('bold called')
        return fn() + ' bold'

    return wrapper

def make_italic(fn):
    def wrapper():
        print('italic called')
        return fn() + ' italic'

    return wrapper

@make_bold
@make_italic
def hello():
    # make_bold will be called first
    # make_italic will return first
    print('hello called')
    return "hello"

print(hello())

```

Output:

```text
bold called
italic called
hello called
<b><i>hello</i></b>
```
