# Python基础
## 一切皆对象
Python中一切皆对象，变量、数据类型、异常、文件操作皆是对象，牢记这一点。Python对代码书写要求比较严格，通过语言标准强迫程序员写出漂亮的代码。
## Python的实现
Python现在流行的是2.6/2.7版本，支持一些3.0的特性，也兼容2.5的语法。Python是脚本语言，其后端有三种实现:
* Cpython   C实现，用的比较多
* Jpython   Java实现
* Ironpython    .NET实现

## 变量
### 强类型动态变量
强类型：变量使用时类型是固定的，不会自动改变类型，比如字符串不能参与算术计算   
动态：可以通过赋值改变类型
### 赋值与引用
使用时直接用'='号赋值，不需要先声明变量类型。推荐在'='两边有一空格。使用的时候直接用变量名即可。
```
# 赋值
var = 5
var = 'this is a string'
f = open('a.txt')
# 引用
print var
new_var = var
```
## 查看文档与帮助
在Python中有以下三种方式可以获得联机帮助，临时参考语法时可以快速查看：
* Bash命令行中用pydoc keywords
* Python解释器中，用help(var)获得对象的详细说明，与pydoc结果一样
* Python解释器中，用dir(var)获得对象的属性和方法列表，结果中大写的是类，小写的是方法

```
# int对象的帮助
pydoc int
# file类的详细帮助
help(file)
# dir对象的方法列表
dir(str)
# 在浏览器中查看python的文档,访问 http://localhost:8000/
$ pydoc -p 8000
```
## 运行Python
### Python脚本
* 同Bash一样Python脚本的第一行也要写上用来解释脚本的程序。中文编程中一般加上coding段，声明所用的字符编码。代码如下：

    ```
    #!/bin/evn python
    # coding: utf8
    # 或
    #!/usr/bin/python
    # coding: utf8
    ```
推荐第一种写法，这种方式是在环境变量中找python解释器的路径，方便多个版本的Python共存。一般系统自带的Python版本较低，但是又被其他程序依赖，升级Python后，会导致其他程序无法使用。一般会单独安装高版本的Python到/usr/local/下面。
* Bash中用python命令打开解释器，在其中直接输入python命令执行，一般用于快速执行命令或短小代码的测试
* python file.py
* `python`提示符中用`execfile("/path/to/file.py")`执行脚本

### Python中调用Bash命令
os模块提供了两个方法调用Bash命令：
* os.system('command') 命令执行结果直接打印到屏幕上。
* var = os.popen('command') 命令执行结果作为返回值。

## 常用内置方法
### print
打印到屏幕。既可简单用作echo，也支持类似C的格式字符串
```
# 末尾加','，不输出换行符，相当于 echo -n
print value1,
# 格式字符串，'%' 后跟的是list类型
print "%s=%s\n" % ('username','yinchuan')
```
### exit
退出Python解释器。需要注意的是exit是Python内置的方法，即函数，使用时要用exit()的形式。
### type
返回参数的数据类型。
```
>>> var='string'
>>> type(var)
<type 'str'>
```
### dir
打印对象的方法与属性。
```
>>> dir(tuple)
['__add__', '__class__', '__contains__', '__delattr__', '__doc__', '__eq__', '__format__', '__ge__', '__getattribute__', '__getitem__', '__getnewargs__', '__getslice__', '__gt__', '__hash__', '__init__', '__iter__', '__le__', '__len__', '__lt__', '__mul__', '__ne__', '__new__', '__reduce__', '__reduce_ex__', '__repr__', '__rmul__', '__setattr__', '__sizeof__', '__str__', '__subclasshook__', 'count', 'index']
# 以'__'开始的是对象的私有方法，一般不用考虑；只看最后面的公有方法即可。
# 如果不加参数,则打印当前module的方法和属性,可以看到当前import的模块
>>> dir()
['__builtins__', '__doc__', '__name__', '__package__', 'mymodule']
```
### raw_input
获取用户输入，类似于Bash的read。
```
>>> raw_input("Waiting for user's input: ")
Waiting for user's input: password
'password'
# 将用户输入保存到变量
>>> var = raw_input("Waiting for user's input: ")
Waiting for user's input: password
>>> print var
password
```
### pass
什么都不做，类似于Bash的':'。
## 控制结构
### if
Python中代码块不用'{ '分界，而是以缩进作为代码块开始与结束的标志。缩进推荐为4个空格。
```
if expr1 == expr2:
    print "equal"
else:
    print "not equal"
# 连接多个表达式，可用 not or
if expr1 == expr2 or expr1 == 1
```
### while
```
i = 0
while i < 10:
    print i
    i += 1
```
### for
```
# range 产生从1开始，步进为2，不包括11的序列
for i in range(1,11,2):
    echo i
```
## 数据类型对象
### int
### str
Python中的str对象是有序的序列，可以通过下标引用，但不能通过下标赋值。
```
>>> var = "this is a string"
>>> print var[0]
t
# str下标从0开始，不允许下标越界，负的下标表示从后面算起
>>> print var[-1]
g
```
str对象支持+和*运算符，+连接字符串，*将字符串复制相应的遍数。
```
>>> var = "a"
>>> print var + "b"
ab
>>> print var * 3
aaa
```
常用的方法有：   
S.format()    返回S的format版本,S中用{}表示占位符,format()的参数依次替换
```
>>> "x {0} {1}".format("first", "zero")
'x first zero'
```
S.join(iterable)    用S连接iterable中的中的元素,常用于合并list,tuple之类
```
>>> 'xx'.join(["1","2"])
'1xx2'
```
```
"".upper "".lower
"".isupper "".islower
"".startswith  "".endswith
" ".lstrip "".rstrip "".strip
```
下标切片
Python中的有序序列均支持下标切片，能够直接截取序列中的部分元素。
```
# 下标切片，从0开始，到3之前，不包括3
>>> var="this is a string"
>>> print var[0:3]
thi
# 下标切片中可以使用负数
>>> print var[0:-1]
this is a strin
```
### list 列表
列表是可写的有序序列，相当于索引数组。
#### 定义与引用
list的定义使用'[ ]'，元素之间用','分隔。引用时用'a[下标]'的形式，可以直接对元素赋值来修改成员。
```
# 定义
>>> a = ['1' , 2 , 3 , '4']
>>> type(a)
<type 'list'>
# 引用
>>> print a[0],a[-1]
1 4
# 修改成员
>>> a[0]=5
>>> print a
[5, 2, 3, '4']
>>>
```
#### 遍历list
```
var = (1,2,3,4)
for i in var:
    print var
```
#### list常用方法
删除   
a.remove('item') 删除指定成员。   
a.pop(index)       删除指定下标的成员，并返回被删除的值。   
del a[index]       用系统内建方法删除指定下标的成员。
插入   
a.insert(index,value) 将元素插入到指定索引处。   
a.append(item) 将元素追加到list末尾。如果item也是list，将作为一个元素插入，即list的成员也可以是list。   
a.extend(list)将list的值加入到a，而不是以一个元素插入。
统计   
len(a)统计元素的个数
### dict 字典
字典是无序的序列，相当于关联数组，用'{key:value'定义，用'var[key]'的形式引用。这里的key,value如果不是变量，要加上引号。
```
>>> var = {'username':'yinchuan','home':'/home/yinchuan'
>>> type(var)
<type 'dict'>
# 引用
>>> print var['username']
yinchuan
```
#### 常用方法
dd.pop()
dd.keys()   dd.values()
dd.has_key()
dd.get(55)      获取key所对应的值，如果不存在返回 None
dd.get(55,'abc')    提供默认值
del dd[55]
#### 遍历
for循环中，遍历的是dict的key，如果要遍历value的话，通过key引用就可以了。
```
# 打印全部dict的成员
>>> for i in var:
...     print "%s=%s" % (i,var[i])
... 
username=yinchuan
home=/home/yinchuan
# 也可以用items()方法获取dict的键值对后再遍历
# str.join()方法的参数是list类型，所以要放在'\[\]'里面
>>> for i,j in var.items():
...     print '='.join([i,j])
... 
username=yinchuan
home=/home/yinchuan
```
### tuple 元组
只读列表，常用于函数返回多个值。方法也不多，用法与list类似，参见dir(tuple)。用小括号定义。
```
>>> a = (1,2,3)
>>> type(a)
<type 'tuple'>
# 定义只有一个元素的 tuple 要加上','，不然会当作算术运算
>>> a = (1,)
>>> type(a)
<type 'tuple'>
```
### set
集合，无序不重复，用得比较少，可以用于去除list中的重复值。
```
>>> a = [11,22,33,11,22,33]
>>> print a
[11, 22, 33, 11, 22, 33]
>>> list(set(a))
[33, 11, 22]
```
## 函数
### 定义
```
def func_name(bb, aa='default'):    # 带默认值的参数，必须放在最后
    cmd
# 示例：
def echo_hello():
    print 'hello world'
    return ok           # 返回值可以是任意类型
                        # 如果要返回多个值，将返回值放在元组里面
```
### 调用
echo_hello(bb=2)
## 文件操作
### open
使用文件之前要先打开，实例化文件。有4个打开模式，如果不加的话，默认是'r'。如果需要以二进制方式打开文件，需要在mode后面加上字符"b"，比如"rb""wb"等。
* 用'r'模式打开一个不存在的文件会报错。
* 用'w'模式打开不存在的文件会创建文件,打开已有内容的文件将清空所有内容.
```
>>> f = open('/path/to/file'[, mode])
```
文件打开模式
<table>
<tr><td>r   </td><td>   read</td></tr>
<tr><td>w   </td><td>   write</td></tr>
<tr><td>a   </td><td>   append</td></tr>
<tr><td>ab  </td><td>   append binary</td></tr>
</table>

### read
1. f.read(size)
    读取sizep字节,如果省略则读取所有内容.   
2. f.readline()
    一次读取一行,包含换行符`\n`。
3. f.readlines()
    读取文件所有内容，以行为单位放到list里面。

```
# 默认以`'r'`模式打开文件.
>>> f = open('a.txt')
# 读取全部内容
>>> print f.read()
first line
second line
>>> f.close()
>>> f = open('a.txt')
>>> print f.readline()
first line
>>> f = open('a.txt')
>>> print f.readlines()
['first line\n', 'second line\n']
```
### seek
文件读取和写入时,文件指针会指向下一个字节,通过`seek`方法定位文件指针.
用法:   
```
seek(offset[, whence]) -> None
```
`offset`是以bytes为单位的偏移量,相对于`whence`.   
`whence`是定位的相对位置,可以是以下3个值:   
    * 0 文件开始处,也是默认值   
    * 1 当前位置   
    * 2 文件结束处

```
# 写入字符串后,从文件头部开始改写
>>> f.write('012345')
>>> f.seek(0)
>>> f.write('678')
# 读取从倒数第4个字节的内容
>>> f.seek(-4, 0)
>>> f.read(1)
```
### write
`f.write('context')`将内容写入到文件，文件不能以'r'模式打开。'w'是写入模式，会覆盖文件原来的内容，相当于'>'。如果要追加需要用'a'模式。如果要写的文件不存在，将新建文件。
```
>>> f = open('a.txt' , 'w')
>>> f.write('line from python')
>>> f.close()
>>> f = open('a.txt')
>>> f.read()
'line from python'
open('a.txt','a')
>>> f.write('line from python in "a" mode')
>>> f.close
>>> f = open('a.txt' , 'r')
>>> print f.read()
line from pythonline from python in "a" mode
```
### close
f.close()   
文件使用完成后记得关闭。
## 类
```
class class_name(father):       # 继承自哪个类，默认为object
    def _private(self,c)        # 私有方法
    def add(self,a,b):          # 类的方法，self用于引入类的实例自身
        """conten of help
           ...
        """                     # 文档字符串，可以当作注释，help(class_name.add)时将显示文档字符串的内容
                                # 定义 class,function,class.method时,第一行语句前
        return a+b
# 使用
abc = class_name()              # abc是class_name的一个实例
```
## 异常
```
try:
    cmd
    raise           # 自定义异常
expect IOError,e:   # e是错误字符串
    cmd
```
## 模块
sys.path    内置模块存于这个路径，第一个元素为当前路径   
所谓module就是以.py结尾的python脚本,脚本中包含变量,类,函数的定义.   
module可以用python/C写成.   
module中的代码在import时会执行,为了加快import的速度,可以将module预编译成字节码,这样在import时会节省编译的时间.   
如何判断module是直接执行,还是被import?可以通过`__name__`参数.
```
if __name__ == ‚__main__‚:
    print(‚This program is being run by itself‚)
else:
    print(‚I am being imported from another module‚)
```
所谓`package`就是存放module的文件夹,其中包含`__init__.py`文件,表示此文件夹包含module.
### sys
import sys      调用模块   
dir(sys)        类型为list，默认值为\$0   
sys.argv        脚本的参数放在这个列表中   
### urllib
参考文档   
* [官方文档][urllib]
* [Python模块学习 --- urllib][urllib1]

[urllib]: http://docs.python.org/2/library/urllib.html
[urllib1]: http://blog.csdn.net/jgood/article/details/5493824
`pythonchallenge`第4题提示用urllib,代码如下   
```
#!/bin/evn python
# coding: utf8
import urllib

# pythonchallenge 第4题的url前缀
base_url = 'http://www.pythonchallenge.com/pc/def/linkedlist.php?nothing='

# 后缀会不断变化
url_suf = '12345'

for i in range(400):
    # 拼接成完整的url
    v_res = urllib.urlopen(base_url + url_suf)
    # url只返回1行字符串,最后一个单词就是下一个url的后缀
    url_suf = v_res.read().split().pop()
    print i, url_suf

# 答案是 peak.html
```
### getopt
C风格的命令行参数解析器
### argparse
2.7中新加.功能强大易用的命令行参数解析器
### random
生成随机数   
`random.random()`   返回[0.0,1.0)之间的随机数   
`random.choice(seq)`  随机返回`seq`中的一个值
### os
与操作系统操作相关,比如文件操作,执行系统命令等   
os.system(command) 执行系统命令,返回值为command的返回值
```
>>> print os.system('date')
Sat Mar  2 11:29:09 CST 2013
0
```
os.sep 返回系统的路径分隔符,linux默认是'/',windows默认是'\'
```
>>> print os.sep
/
```
## 使用PyGObject开发Gtk3.0图形程序
### 示例程序`helloworld.py`
窗口中有一个button,点击之后在终端打印"hello world"   
参考文档
* [官方sample][helloworld]

[helloworld]: https://python-gtk-3-tutorial.readthedocs.org/en/latest/introduction.html#simple-example
```
#!/bin/env python
# coding: utf8
# helloworld
#

from gi.repository import Gtk

window = Gtk.Window(type=Gtk.WindowType.TOPLEVEL)
# 连接主循环退出函数,不然窗口关闭时,进程不会退出
window.connect("destory", Gtk.main_quit)

# 按钮的回调函数
def onButtonPressed(button):
    print "Hello World!"
# 生成button实例,连接回调函数,添加到window
button = Gtk.Button("Click me!")
button.connect("clicked", onButtonPressed)
window.add(button)

# 显示所有widget,开始主循环
window.show_all()
Gtk.main()
```
