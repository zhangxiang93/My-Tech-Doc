### 装饰器是什么
装饰器本质上是一个 `Python` 函数或类，它可以让其他函数或类在不需要做任何代码修改的前提下增加额外功能，装饰器的返回值也是一个函数/类对象。概括的讲，装饰器的作用就是为已经存在的对象添加额外的功能。


### 例子
先看一个，下面例子是把运行函数信息加入日志记录
```
def use_logging(func):
    logging.warn("%s is running" % func.__name__)
    func()

def foo():
    print('i am foo')

use_logging(foo)
```
这么写没有问题，也不会重复，但是我们调用的时候不再是调用真正的业务逻辑 `foo` 函数，而是换成了 `use_logging` 函数，这就破坏了原有的代码结构。
简单实现
```
def use_logging(func):

    def wrapper():
        logging.warn("%s is running" % func.__name__)
        return func()   # 把 foo 当做参数传递进来时，执行func()就相当于执行foo()
    return wrapper

def foo():
    print('i am foo')

foo = use_logging(foo)  # 因为装饰器 use_logging(foo) 返回的时函数对象 wrapper，这条语句相当于  foo = wrapper
foo()                   # 执行foo()就相当于执行 wrapper()
```
`use_logging` 就是一个装饰器，它一个普通的函数，它把执行真正业务逻辑的函数 `func` 包裹在其中，看起来像 `foo` 被 `use_logging` 装饰了一样，`use_logging` 返回的也是一个函数，这个函数的名字叫 `wrapper`。在这个例子中，函数进入和退出时 ，被称为一个横切面，这种编程方式被称为面向切面的编程。
但是是不是很不美，没问题，`python`还有神器，`@`语法糖出场


### @语法糖

##### 无参数用法
上面例子可以这么写
```
def use_logging(func):

    def wrapper():
        logging.warn("%s is running" % func.__name__)
        return func()
    return wrapper

@use_logging
def foo():
    print("i am foo")

foo()
```
是不是好看多了，还少写了一步。这样，我们就提高了程序的可重复利用性，并增加了程序的可读性。

##### 带参数用法
非字典参数
```
def use_logging(func):

    def wrapper(*args):
        logging.warn("%s is running" % func.__name__)
        return func()
    return wrapper

@use_logging
def foo(name, age):
    print("i am foo")

foo()
```
带字典参数
```
def use_logging(func):

    def wrapper(*args, **kwargs):
        # args是一个数组，kwargs一个字典
        logging.warn("%s is running" % func.__name__)
        return func(*args, **kwargs)
    return wrapper

@use_logging
def foo(name, age=None, height=None):
    print("i am foo")

foo()
```

字典带参数
```
def use_logging(level):
    def decorator(func):
        def wrapper(*args, **kwargs):
            if level == "warn":
                logging.warn("%s is running" % func.__name__)
            elif level == "info":
                logging.info("%s is running" % func.__name__)
            return func(*args)
        return wrapper

    return decorator

@use_logging(level="warn")
def foo(name='foo'):
    print("i am %s" % name)

foo()
```
这里实际就是对原有函数多了一层封装，来传递参数。

##### 类装饰器
装饰器不仅可以是函数，还可以是类，相比函数装饰器，类装饰器具有灵活度大、高内聚、封装性等优点。使用类装饰器主要依靠类的`__call__`方法，当使用 `@ `形式将装饰器附加到函数上时，就会调用此方法。
```
class Foo(object):
    def __init__(self, func):
        self._func = func

    def __call__(self):
        print ('class decorator runing')
        self._func()
        print ('class decorator ending')

@Foo
def bar():
    print ('bar')

bar()
```
装饰器虽好，但是也有缺点，原函数的元信息不见了，比如函数的`docstring`、`__name__`、参数列表，先看例子：
```
# 装饰器
def logged(func):
    def with_logging(*args, **kwargs):
        print func.__name__      # 输出 'with_logging'
        print func.__doc__       # 输出 None
        return func(*args, **kwargs)
    return with_logging

# 函数
@logged
def f(x):
   """does some math"""
   return x + x * x

logged(f)
```
这里`f`的元信息被`with_logging`取代了
解决这个问题，需要`functools.wraps`
##### functools.wraps
```
from functools import wraps
def logged(func):
    @wraps(func)
    def with_logging(*args, **kwargs):
        print func.__name__      # 输出 'f'
        print func.__doc__       # 输出 'does some math'
        return func(*args, **kwargs)
    return with_logging

@logged
def f(x):
   """does some math"""
   return x + x * x
```
此时就可以正常输出`f`的元信息了。

### 装饰器顺序
```
@a
@b
@c
def f ():
    pass
```
执行顺序从里到外
```
f = a(b(c(f)))
```
