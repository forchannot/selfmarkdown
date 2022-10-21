#### 字符串的处理

- **Python 中单引号 ' 和双引号 " 使用完全相同。**
- 使用三引号(''' 或 """)可以指定一个多行字符串。
- 转义符 \。
- 反斜杠可以用来转义，使用 r 可以让反斜杠不发生转义。 如 **r"this is a line with \n"** 则 \n 会显示，并不是换行。
- 按字面意义级联字符串，如 **"this " "is " "string"** 会被自动转换为 **this is string**。
- 字符串可以用 + 运算符连接在一起，用 * 运算符重复。
- Python 中的字符串有两种索引方式，从左往右以 0 开始，从右往左以 -1 开始。**（可以混用，在同一个语句中一起用）**
- Python 中的字符串不能改变。**（啥意思呢）**
- Python 没有单独的字符类型，一个字符就是长度为 1 的字符串。**（啥意思呢）**
- 字符串的截取的语法格式如下：变量[头下标:尾下标:步长]

```python
str='123456789'

print(str)                 # 输出字符串
print(str[0:-1])           # 输出第一个到倒数第二个的所有字符
print(str[0])              # 输出字符串第一个字符
print(str[2:5])            # 输出从第三个开始到第五个的字符
print(str[2:])             # 输出从第三个开始后的所有字符
print(str[1:5:2])          # 输出从第二个开始到第五个且每隔一个的字符（步长为2）
print(str * 2)             # 输出字符串两次
print(str + '你好')         # 连接字符串

print('------------------------------')

print('hello\nrunoob')      # 使用反斜杠(\)+n转义特殊字符
print(r'hello\nrunoob')     # 在字符串前面添加一个 r，表示原始字符串，不会发生转义
```

#### Python3 基本数据类型

Python 中的变量不需要声明。每个变量在使用前都必须赋值，变量赋值以后该变量才会被创建。

在 Python 中，变量就是变量，它没有类型，我们所说的"类型"是变量所指的内存中对象的类型。

#### 标准数据类型

Python3 中有六个标准的数据类型：

- Number（数字）
- String（字符串）
- List（列表）
- Tuple（元组）
- Set（集合）
- Dictionary（字典）

Python3 的六个标准数据类型中：

- **不可变数据（3 个）：**Number（数字）、String（字符串）、Tuple（元组）；
- **可变数据（3 个）：**List（列表）、Dictionary（字典）、Set（集合）。

内置的 type() 函数可以用来查询变量所指的对象类型。

```python
>>> a, b, c, d = 20, 5.5, True, 4+3j
>>> print(type(a), type(b), type(c), type(d))
<class 'int'> <class 'float'> <class 'bool'> <class 'complex'>
```

##### 7月17日学习笔记

```python
a=eval(input("请输入："))
input函数的提示性文字是可选的
eval函数用于去掉双引号
```

##### 7月20日学习笔记

打开IDLE，点击Ctrl+N打开一个新窗口，输入语句并保存，使用快键建F5即可运行该程序

n启动IDLE所显示的环境是Python交互式运行环境，在>>>提示符后输入代码即可运行，输入exit()或者quit()可以退出，没有>>>的行表示运行结果。

```python
a=24
print（a,end="."）
结果输出为24.(而且不会自动换行)默认的print函数会自动换行
```



##### IDLE的快捷方式

```
ctrl+N:在交互界面下，启动文件编辑器
ctrl+Q:推出编辑器
alt+3:在文本编辑器里，注释选定文本
alt+4:解除注释
alt+Q:格式化布局
f5:执行程序
```



8月9日

选中xxx.jpg前面的xxx的正则表达式：

```
.+[^(.jpg)]
```

这是我自己琢磨出来的，其中（.jpg）代表群组，`[^(.jpg)]`代表不选.jpg，.+代表选取一个或多个字符。



9月5日

与 C 字符串不同的是，Python 字符串不能被改变。向一个索引位置赋值，比如word[0] = 'm'会导致错误。

9月9日

### global全局变量的用法

函数的作用域，局部变量和全局变量

全局变量在函数里面使用的时候要在前面使用关键字global声明。

```
global a
```

如果未使用保留字global声明，即使名称相同，也不是全局变量。（这是一个重要的地方，不要想当然认为在函数外面声明的变量就是全局变量，想要把它作为全局变量是要在函数里面用global声明的）

这里联想到咱们单片机课设的时候好像就出现了这样的问题，这种要求可能在许多别的编程语言里面都有要求吧。单片机使用C语言，应该也不是说声明在函数外的变量就可以作为全局变量。（有待核实）

9月11日

## 9月17日

今天是周六，好像没几天就要考试了。我来到8教学习，或者说开会，但是截止9：22除了我还没有别人

## range()函数

如果你需要遍历数字序列，可以使用内置range()函数。它会生成数列range(5)输出01234

还可以指定区间的值range(5,9)输出5，6，7，8

也可以使range以指定数字开始并指定不同的增量(甚至可以是负数，有时这也叫做'步长')

range(0, 10, 3)输出0369

##### 区分break和continue

while 语句代码执行过程：

<img src="https://static.runoob.com/images/mix/python-while.webp" style="zoom: 33%;" />

for 语句代码执行过程：

![](https://www.runoob.com/wp-content/uploads/2014/05/break-continue-536.png)

**break** 语句可以跳出 for 和 while 的循环体。如果你从 for 或 while 循环中终止，任何对应的循环 else 块将不执行。

**continue** 语句被用来告诉 Python 跳过当前循环块中的剩余语句，然后继续进行下一轮循环。

- 按我的理解break就像一个大杀器，只要使用它，这个内层的循环就整体结束了。

- continue就像一个筛选器，遇到它的那一轮循环就会很倒霉，直接跳过后面的东西，不管还剩多少，跳到下一轮循环去

循环语句可以有 else 子句，它在穷尽列表(以for循环)或条件变为 false (以while循环)导致循环终止时被执行，但循环被 break 终止时不执行。相当于对循环正常结束的一种奖励

### 参数传递

在 python 中，类型属于对象，对象有不同类型的区分，变量是没有类型的：

***这点就和C和Java很不一样啊***

```
a=[1,2,3]

a="Runoob"
```

以上代码中，**[1,2,3]** 是 List 类型，**"Runoob"** 是 String 类型，而变量 a 是没有类型，她仅仅是一个对象的引用（一个指针），可以是指向 List 类型对象，也可以是指向 String 类型对象。

### 可更改(mutable)与不可更改(immutable)对象

在 python 中，strings(字符串), tuples(元组), 和 numbers(数字) 是不可更改的对象，而 list(列表),dict(字典) 等则是可以修改的对象。

- **不可变类型：**变量赋值 **a=5** 后再赋值 **a=10**，这里实际是新生成一个 int 值对象 10，再让 a 指向它，而 5 被丢弃，不是改变 a 的值，相当于新生成了 a。
- **可变类型：**变量赋值 **la=[1,2,3,4]** 后再赋值 **la[2]=5** 则是将 list la 的第三个元素值更改，本身la没有动，只是其内部的一部分值被修改了。

python 函数的参数传递：

- **不可变类型：**类似 C++ 的值传递，如整数、字符串、元组。如 fun(a)，传递的只是 a 的值，没有影响 a 对象本身。如果在 fun(a) 内部修改 a 的值，则是新生成一个 a 的对象。
- **可变类型：**类似 C++ 的引用传递，如 列表，字典。如 fun(la)，则是将 la 真正的传过去，修改后 fun 外部的 la 也会受影响

python 中一切都是对象，严格意义我们不能说值传递还是引用传递，我们应该说传不可变对象和传可变对象。

### python 传不可变对象实例

通过 **id()** 函数来查看内存地址变化：

```python
def change(a):
    print(id(a))   # 指向的是同一个对象
    a=10
    print(id(a))   # 一个新对象

a=1
print(id(a))
change(a)
```

以上实例输出结果为：

```
4379369136
4379369136
4379369424
```

可以看见在调用函数前后，形参和实参指向的是同一个对象（对象 id 相同），在函数内部修改形参后，形参指向的是不同的 id。

### 传可变对象实例

可变对象在函数里修改了参数，那么在调用这个函数的函数里，原始的参数也被改变了。例如：

```python
#!/usr/bin/python3

# 可写函数说明

def changeme( mylist ):
   "修改传入的列表"
   mylist.append([1,2,3,4])
   print ("函数内取值: ", mylist)
   return

# 调用changeme函数

mylist = [10,20,30]
changeme( mylist )
print ("函数外取值: ", mylist)
```

传入函数的和在末尾添加新内容的对象用的是同一个引用。故输出结果如下：

```
函数内取值:  [10, 20, 30, [1, 2, 3, 4]]
函数外取值:  [10, 20, 30, [1, 2, 3, 4]]
```

#### 元组：一个星号表示元组

```python
(60, 50)
```

#### 字典：两个星号表示字典（键值对）

```python
{'a': 2, 'b': 3}
```

### 函数中星号的意思（元组或字典）

一个星号表示[元组](https://so.csdn.net/so/search?q=元组&spm=1001.2101.3001.7020)，两个星号表示字典（键值对）

也就是说在这个参数前面加一个星号，那么在函数内部，这个参数就表示一个元组**（元组和列表除了元组不能改变，其他完全一样，所以里面的元素是可以重复的）**

在这个参数前面加两个星号，那么在函数内部，这个参数就表示一个字典

#### 元组

```python
def demo(a, *b):
    print(a)#输出得到1
    print(b)#输出得到(2, 3, 4, 5)

demo(1, 2, 3, 4, 5)


def demo(a, *b):
   print(a)  # 输出得到1
   print(b)  # 输出得到(2, 3, 4, 5, 4, 4, 2, 1)

demo(1, 2, 3, 4, 5,4,4,2,1)
```

#### 字典

```python
def demo(a, **b):
    print(a)#输出得到1
    print(b)#输出得到{'m': 2, 'n': 3, 'x': 4, 'y': 5, 'z': 7, 'eating': 8}

demo(1, m=2,n=3,x=4,y=5,z=7,eating=8)
```

#### 这	def f(a,b,*,c):	的星号是啥意思，有什么用吗

##### 作用就是让星号 * 后的参数必须用关键字传入吧

声明函数时，参数中星号 * 可以单独出现，例如:

```python
def f(a,b,*,c):
    return a+b+c
```

如果单独出现星号 *，则星号 * 后的参数必须用关键字传入：

```python
>>> def f(a,b,*,c):
...     return a+b+c
... 
>>> f(1,2,3)   # 报错
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: f() takes 2 positional arguments but 3 were given
>>> f(1,2,c=3) # 正常
6
>>>
```

#### 菜鸟教程下面别人的笔记

##### Python 文档字符串(DocStrings)

##### 话说这种方式和注释有什么区别吗

​		可以通过  `函数名.__doc__` 的方式来显示函数的说明文档，感觉这个如果在阅读比较大的程序时应该会有用，同时也在提示自己在写函数时注意添加文档说明。

```python
def add(a,b):
    "这是 add 函数文档"
    return a+b

print (add.__doc__)
```

输出结果为：

```
这是 add 函数文档
```

> 更多内容可参考：[Python 文档字符串(DocStrings)](https://www.runoob.com/w3cnote/python-docstrings.html)

[Mr.Wu](javascript:;)  Mr.Wu 928***263@qq.com4年前 (2018-07-20)

##### 函数返回值的注意事项: 

不同于 C 语言，Python 函数可以返回多个值，多个值以**元组**的方式返回:

```python
def fun(a,b):    
    "返回多个值，结果以元组形式表示"
    return a,b,a+b
print(fun(1,2))
```

输出结果为：

```
(1, 2, 3)
```

[Mr.Wu](https://www.runoob.com/note/29889)  Mr.Wu 928***263@qq.com4年前 (2018-07-20)

##### 关于global关键字的细节

对于变量作用域，变量的访问以 **L（Local） –> E（Enclosing） –> G（Global） –>B（Built-in）** 的规则查找，即：在局部找不到，便会去局部外的局部找（例如闭包），再找不到就会去全局找，再者去内建中找。

**global** 关键字会跳过中间层直接将嵌套作用域内的局部变量变为全局变量:

测试代码如下:

```python
num = 20
def outer():
    num = 10
    def inner():
        global num
        print (num)
        num = 100
        print (num)
    inner()
    print(num)
outer()
print (num)
```

​     结果如下：

```
20
100
10
100
```

[爱睡觉的猫](javascript:;)  爱睡觉的猫 199***09662@163.com4年前 (2019-01-16)

```python
a = 10  # 此处a是声明全部变量
def sum ( n ) :
    a = 20  # 此处a是声明局部变量，局部变量会随着方法出栈而消失(闭包除外)
    n += a  # 此处调用的是局部变量a
    print ('a = ', a, end = ' , ' )
    print ( 'n = ', n )
sum(3)
print ('a = ', a, end = '' )
输出结果是：
a =  20 , n =  23
a =  10
#################
a = 10
def sum ( n ) :
   n += a  # 此处引用全局变量a, 注意：这个函数内并没有声明局部变量a
   a = 11  # 此处修改全局变量a, 必然会报错！如要函数内修改全部变量，用global声明就不会报错
   print ('a = ', a, end = ' , ' )
   print ( 'n = ', n )
```

[codeduck1](javascript:;)  codeduck1 cod***ck@aliyun.com2年前 (2021-03-23)

#### python保留字

```python
>>> import keyword
>>> keyword.kwlist
['False', 'None', 'True', 'and', 'as', 'assert', 'break', 'class', 'continue', 'def', 'del', 'elif', 'else', 'except', 'finally', 'for', 'from', 'global', 'if', 'import', 'in', 'is', 'lambda', 'nonlocal', 'not', 'or', 'pass', 'raise', 'return', 'try', 'while', 'with', 'yield']
```



#### 注释

Python中单行注释以 **#** 开头

多行注释可以用多个 # 号，还有  ''' 和 """

```python
# 第一个注释
# 第二个注释
 
'''
第三注释
第四注释
'''
 
"""
第五注释
第六注释
"""
```

#### 行与缩进

缩进：indent，缩进错误：unindent

#### 多行语句

Python 通常是一行写完一条语句，但如果语句很长，我们可以使用反斜杠 \ 来实现多行语句，例如：

```python
total = item_one + \
        item_two + \
        item_three
```

在  [], {}, 或 () 中的多行语句，不需要使用反斜杠 \，例如：

```python
total = ['item_one', 'item_two', 'item_three',
        'item_four', 'item_five']
```

#### 数字(Number)类型

python中数字有四种类型：整数、布尔型、浮点数和复数。

- **int** (整数), 如 1, 只有一种整数类型 int，表示为长整型，没有 python2 中的 Long。
- **bool** (布尔), 如 True。
- **float** (浮点数), 如 1.23、3E-2
- **complex** (复数), 如 1 + 2j、 1.1 + 2.2j

#### 转义符/

反斜杠可以用来转义，使用 r 可以让反斜杠不发生转义。 如 **r"this is a line with \n"** 则 \n 会显示，并不是换行。

```python
print('hello\nrunoob')      # 使用反斜杠(\)+n转义特殊字符
print(r'hello\nrunoob')     # 在字符串前面添加一个 r，表示原始字符串，不会发生转义
输出结果

hello
runoob

hello\nrunoob
```

### 9月19日

#### python中函数的定义和调用的先后顺序问题

https://blog.csdn.net/dugushangliang/article/details/89016588

调用函数之前得知道有这个函数，所以执行代码前需要有要用到的函数的定义。

程序执行的时候，读取到函数的定义的时候，就是记录下函数的名单，知道有这么些函数，但是不看函数里面的内容，当需要执行函数的时候才去读取这个函数里面的内容。

**我来总结一下**：python的运行逻辑是按顺序从上往下，遇到函数只记录下来有这个函数，而不去看函数里面具体内容，当调用函数的时候回去找这个函数所在位置，运行函数里面的语句。

#### 文字格式之诗文风

```python
# Example_5_1.py
txt = '''
人生得意须尽欢，莫使金樽空对月。
天生我材必有用，千金散尽还复来。
'''
linewidth = 30  # 预定的输出宽度

def lineSplit(line):
    plist = [',', '!', '?', '，', '。', '！', '？']
    for p in plist:
        line = line.replace(p, '\n')
    return line.split('\n')		#split以(空行)来分割字符串，以列表类型返回
    
def linePrint(line):
    global linewidth
    print(line.center(linewidth, chr(12288)))

newlines = lineSplit(txt)
for newline in newlines:
    linePrint(newline)

```

## 列表

Python中列表是可变的，这是它区别于字符串和元组的最重要的特点，一句话概括即：列表可以修改，而字符串和元组不能。

### Python3 基本数据类型

Python 中的变量不需要声明。每个变量在使用前都必须赋值，变量赋值以后该变量才会被创建。

在 Python 中，变量就是变量，它没有类型，我们所说的"类型"是变量所指的内存中对象的类型。

等号（=）用来给变量赋值。

等号（=）运算符左边是一个变量名,等号（=）运算符右边是存储在变量中的值。

#### 标准数据类型

Python3 中有六个标准的数据类型：

- Number（数字）
- String（字符串）
- List（列表）
- Tuple（元组）
- Set（集合）
- Dictionary（字典）

Python3 的六个标准数据类型中：

- **不可变数据（3 个）：**Number（数字）、String（字符串）、Tuple（元组）；
- **可变数据（3 个）：**List（列表）、Dictionary（字典）、Set（集合）。

#### Number（数字）

Python3 支持 **int、float、bool、complex（复数）**。

在Python 3里，只有一种整数类型 int，表示为长整型，没有 python2 中的 Long。

像大多数语言一样，数值类型的赋值和计算都是很直观的。

内置的 type() 函数可以用来查询**变量所指的对象类型**。

```python
>>> a, b, c, d = 20, 5.5, True, 4+3j
>>> print(type(a), type(b), type(c), type(d))
<class 'int'> <class 'float'> <class 'bool'> <class 'complex'>
```

isinstance 和 type 的区别在于：

- type()不会认为子类是一种父类类型。
- isinstance()会认为子类是一种父类类型。



**注意：**Python3 中，bool 是 int 的子类，True 和 False 可以和数字相加， True==1、False==0 会返回 **True**，但可以通过 is 来判断类型。

**注意：**

- 1、Python可以同时为多个变量赋值，如a, b = 1, 2。
- 2、一个变量可以通过赋值指向不同类型的对象。
- 3、数值的除法包含两个运算符：/ 返回一个浮点数，// 返回一个整数。
- 4、在混合计算时，Python会把整型转换成为浮点数。

### String（字符串）

与 C 字符串不同的是，Python 字符串不能被改变。向一个索引位置赋值，比如word[0] = 'm'会导致错误。

**注意：**

- 1、反斜杠可以用来转义，使用r可以让反斜杠不发生转义。
- 2、字符串可以用+运算符连接在一起，用*运算符重复。
- 3、Python中的字符串有两种索引方式，从左往右以0开始，从右往左以-1开始。
- 4、Python中的字符串不能改变。

### List（列表）

List（列表） 是 Python 中使用最频繁的数据类型。

列表可以完成大多数集合类的数据结构实现。列表中元素的类型可以不相同，它支持数字，字符串甚至可以包含列表（所谓嵌套）。

列表是写在方括号 [] 之间、用逗号分隔开的元素列表。

和字符串一样，列表同样可以被索引和截取，列表被截取后返回一个包含所需元素的新列表。

与Python字符串不一样的是，列表中的元素是可以改变的

**注意：**

- 1、List写在方括号之间，元素用逗号隔开。
- 2、和字符串一样，list可以被索引和切片。
- 3、List可以使用+操作符进行拼接。
- 4、List中的元素是可以改变的。

Python 列表截取可以接收第三个参数，参数作用是截取的步长，如果第三个参数为负数表示逆向读取，实例用于翻转字符串

### Tuple（元组）

元组（tuple）与列表类似，不同之处在于元组的元素不能修改。元组写在小括号 () 里，元素之间用逗号隔开。

元组中的元素类型也可以不相同

元组与字符串类似，可以被索引且下标索引从0开始，-1 为从末尾开始的位置。也可以进行截取（看上面，这里不再赘述）。

其实，可以把字符串看作一种特殊的元组。

虽然tuple的元素不可改变，但它可以包含可变的对象，比如list列表。

构造包含 0 个或 1 个元素的元组比较特殊，所以有一些额外的语法规则：

```
tup1 = ()    # 空元组
tup2 = (20,) # 一个元素，需要在元素后添加逗号
```

string、list 和 tuple 都属于 sequence（序列）。

**注意：**

- 1、与字符串一样，元组的元素不能修改。
- 2、元组也可以被索引和切片，方法一样。
- 3、注意构造包含 0 或 1 个元素的元组的特殊语法规则。
- 4、元组也可以使用+操作符进行拼接。

### Set（集合）

集合（set）是由一个或数个形态各异的大小整体组成的，构成集合的事物或对象称作元素或是成员。

基本功能是进行成员关系测试和删除重复元素。

可以使用大括号 { } 或者 set() 函数创建集合，注意：创建一个空集合必须用 set() 而不是 { }，因为 { } 是用来创建一个空字典。

创建格式：

```python
parame = {value01,value02,...}
或者
set(value)
```

```python
#!/usr/bin/python3

sites = {'Google', 'Taobao', 'Runoob', 'Facebook', 'Zhihu', 'Baidu'}

print(sites)   # 输出集合，重复的元素被自动去掉

# 成员测试
if 'Runoob' in sites :
    print('Runoob 在集合中')
else :
    print('Runoob 不在集合中')


# set可以进行集合运算
a = set('abracadabra')
b = set('alacazam')

print(a)

print(a - b)     # a 和 b 的差集

print(a | b)     # a 和 b 的并集

print(a & b)     # a 和 b 的交集

print(a ^ b)     # a 和 b 中不同时存在的元素
```

输出结果为

```python
{'Zhihu', 'Baidu', 'Taobao', 'Runoob', 'Google', 'Facebook'}
Runoob 在集合中
{'b', 'c', 'a', 'r', 'd'}
{'r', 'b', 'd'}
{'b', 'c', 'a', 'z', 'm', 'r', 'l', 'd'}
{'c', 'a'}
{'z', 'b', 'm', 'r', 'l', 'd'}
```

### Dictionary（字典）

字典（dictionary）是Python中另一个非常有用的内置数据类型。

列表是有序的对象集合，字典是无序的对象集合。两者之间的区别在于：字典当中的元素是通过键来存取的，而不是通过偏移存取。

字典是一种映射类型，字典用 { } 标识，它是一个无序的 **键(key) : 值(value)** 的集合。

键(key)必须使用不可变类型。

在同一个字典中，键(key)必须是唯一的。

用法：

```python
#!/usr/bin/python3

dict = {}
dict['one'] = "1 - 菜鸟教程"
dict[2]     = "2 - 菜鸟工具"

tinydict = {'name': 'runoob','code':1, 'site': 'www.runoob.com'}


print (dict['one'])       # 输出键为 'one' 的值
print (dict[2])           # 输出键为 2 的值
print (tinydict)          # 输出完整的字典
print (tinydict.keys())   # 输出所有键
print (tinydict.values()) # 输出所有值
```

以上实例输出结果：

```python
1 - 菜鸟教程
2 - 菜鸟工具
{'name': 'runoob', 'code': 1, 'site': 'www.runoob.com'}
dict_keys(['name', 'code', 'site'])
dict_values(['runoob', 1, 'www.runoob.com'])
```

构造函数 dict() 可以直接从键值对序列中构建字典如下：

```python
>>> dict([('Runoob', 1), ('Google', 2), ('Taobao', 3)])
{'Runoob': 1, 'Google': 2, 'Taobao': 3}
>>> {x: x**2 for x in (2, 4, 6)}
{2: 4, 4: 16, 6: 36}
>>> dict(Runoob=1, Google=2, Taobao=3)
{'Runoob': 1, 'Google': 2, 'Taobao': 3}
```

`{x: x**2 for x in (2, 4, 6)}` 该代码使用的是字典推导式

**注意：**

- 1、字典是一种映射类型，它的元素是键值对。
- 2、字典的关键字必须为不可变类型，且不能重复。
- 3、创建空字典使用 **{ }**。


------
#### 菜鸟教程下面网友的补充
python 与 C 语言和 Java 语言的一点不同，表现在它的变量不需要声明变量类型，这是因为像 C 语言和 Java 语言来说，它们是静态的，而 python 是动态的，变量的类型由赋予它的值来决定，例如：
```python
>>> a = 1
>>> a = 1.001
>>> a = "python"
>>> print(a)
python
>>> 
```

第一次为变量 a 赋值为整型，第二次赋值是浮点数，第三次是一个字符串，最后输出时只保留了最后一次的赋值。

[hellowqp](javascript:;)  hellowqp wqp***a@foxmail.com5年前 (2017-07-08)

------

type 是用于求一个未知数据类型对象，而 isinstance 是用于判断一个对象是否是已知类型。

type 不认为子类是父类的一种类型，而isinstance会认为子类是父类的一种类型。

可以用 isinstance 判断子类对象是否继承于父类，type 不行。

综合以上几点，type 与 isinstance 虽然都与数据类型相关，但两者其实用法不同，type 主要用于判断未知数据类型，isinstance 主要用于判断 A 类是否继承于 B 类：

```
# 判断子类对象是否继承于父类
class father(object):
    pass
class son(father):
    pass
if __name__ == '__main__':
    print (type(son())==father)
    print (isinstance(son(),father))
    print (type(son()))
    print (type(son))
```

运行结果：

```
False
True
<class '__main__.son'>
<type 'type'>
```

[燕春](javascript:;)  燕春 zqs***306010@qq.com [ 参考地址](http://blog.csdn.net/cn_wk/article/details/51314238)5年前 (2017-09-15)

### **集合与字典**

**无序：**集合是无序的，所以不支持索引；字典同样也是无序的，但由于其元素是由键（key）和值（value）两个属性组成的键值对，可以通过键（key）来进行索引

**元素唯一性：**集合是无重复元素的序列，会自动去除重复元素；字典因为其key唯一性，所以也不会出现相同元素

[好好学习天天向上](javascript:;)  好好学习天天向上 522***154@qq.com5年前 (2018-03-01)

------

此处延伸下变量和对象之间的关系：

- 赋值操作，本质是创建引用
- 变量是变量，对象是对象，当将某个对象赋值给某个变量时，可以认为是创建了变量对该对象的引用
- 变量没有数据类型之说，只有对象有，即变量不是直接代表对象或对象占用的内存空间
- Python中，变量无需提前声明，无需指定其数据类型，其表现完全是动态的，其所为的数据类型决定于当前该变量所引用的对象的数据类型
- 所谓变量对对象的引用，本质是创建了变量指向对象内存空间的指针
- 对象内存空间，一般最起码有类型和当前被引用次数这两个信息，类型记录了该对象的数据类型，被引用次数记录了该对象内存空间被变量引用的次数
- 当某对象的被引用次数为0时，Python便会自动回收该对象内存空间

比如下面的

```python
a=10
a='122'
a=[1,2,3]
del a
```

此时，a在不同的赋值代码行中，引用的对象类型不同，相当于在不断改变a引用的对象，最后当把a变量删除时，其实本质只是删除了a变量名，但由于a引用的[1,2,3]对象，因为a被删除，其被引用次数变为0，也就自动被Python回收，最终表现就是del a时，[1,2,3]也被删除了。

另外一个小知识是，Python为提升代码执行和内存分配效率，会对一些常用的对象提前创建好，并常驻内存，比如下面：

```python
id(4) #不管运行多少次该代码，其返回的值均不变，因为python会保持一些常用的数字常驻内存，不会每次都重新分配内存空间
id('hello world') #每次运行，返回的值均会发生变化，因为每次运行，相当于都在重新分配内存空间
```

[闫伟超](javascript:;)  闫伟超 yif***chaoran@163.com2年前 (2021-02-20)

## 9月19日

### 文件和数据格式化

#### open() 方法

Python open() 方法用于打开一个文件，并返回文件对象。

在对文件进行处理过程都需要使用到这个函数，如果该文件无法被打开，会抛出 OSError。

**注意：**使用 open() 方法一定要保证关闭文件对象，即调用 close() 方法。

open() 函数常用形式是接收两个参数：文件名(file)和模式(mode)。

```python
open(file, mode='r')
```

完整的语法格式为：

```python
open(file, mode='r', buffering=-1, encoding=None, errors=None, newline=None, closefd=True, opener=None)
```

参数说明:

- file: 必需，文件路径（相对或者绝对路径）。
- mode: 可选，文件打开模式
- buffering: 设置缓冲
- encoding: 一般使用utf8
- errors: 报错级别
- newline: 区分换行符
- closefd: 传入的file参数类型
- opener: 设置自定义开启器，开启器的返回值必须是一个打开的文件描述符。

mode 参数有：

| 模式 | 描述                                                         |
| :--: | ------------------------------------------------------------ |
|  t   | 文本模式 (默认)。                                            |
|  x   | 写模式，新建一个文件，如果该文件已存在则会报错。             |
|  b   | 二进制模式。                                                 |
|  +   | 打开一个文件进行更新(可读可写)。                             |
|  U   | 通用换行模式（**Python 3 不支持**）。                        |
|  r   | 以只读方式打开文件。文件的指针将会放在文件的开头。这是默认模式。 |
|  rb  | 以二进制格式打开一个文件用于只读。文件指针将会放在文件的开头。这是默认模式。一般用于非文本文件如图片等。 |
|  r+  | 打开一个文件用于读写。文件指针将会放在文件的开头。           |
| rb+  | 以二进制格式打开一个文件用于读写。文件指针将会放在文件的开头。一般用于非文本文件如图片等。 |
|  w   | 打开一个文件只用于写入。如果该文件已存在则打开文件，并从开头开始编辑，即原有内容会被删除。如果该文件不存在，创建新文件。 |
|  wb  | 以二进制格式打开一个文件只用于写入。如果该文件已存在则打开文件，并从开头开始编辑，即原有内容会被删除。如果该文件不存在，创建新文件。一般用于非文本文件如图片等。 |
|  w+  | 打开一个文件用于读写。如果该文件已存在则打开文件，并从开头开始编辑，即原有内容会被删除。如果该文件不存在，创建新文件。 |
| wb+  | 以二进制格式打开一个文件用于读写。如果该文件已存在则打开文件，并从开头开始编辑，即原有内容会被删除。如果该文件不存在，创建新文件。一般用于非文本文件如图片等。 |
|  a   | 打开一个文件用于追加。如果该文件已存在，文件指针将会放在文件的结尾。也就是说，新的内容将会被写入到已有内容之后。如果该文件不存在，创建新文件进行写入。 |
|  ab  | 以二进制格式打开一个文件用于追加。如果该文件已存在，文件指针将会放在文件的结尾。也就是说，新的内容将会被写入到已有内容之后。如果该文件不存在，创建新文件进行写入。 |
|  a+  | 打开一个文件用于读写。如果该文件已存在，文件指针将会放在文件的结尾。文件打开时会是追加模式。如果该文件不存在，创建新文件用于读写。 |
| ab+  | 以二进制格式打开一个文件用于追加。如果该文件已存在，文件指针将会放在文件的结尾。如果该文件不存在，创建新文件用于读写。 |

默认为文本模式，如果要以二进制模式打开，加上 b 。

发现

```python
a=['1','2','3']
a=','.join(a)
print(a)

显示
1,2,3
```



```python
a=['1','2','3']
#a=','.join(a)
print(a)

显示
['1', '2', '3']
```

还发现print函数在IDLE交互式编程窗口里面输出字符串带‘	’引号

在文件编程里面输出字符串不带引号

join方法会把原来的元素隔开，变成一个新的字符串，所以输出的是字符串

```python
f=open('E:/Python_Learning/2-行文代码/第7章/finance - 副本.csv','r',encoding='utf-8-sig')
ls=[]
for line in f:
    ls.append(line.strip('\n').split(','))
f.close()
print(ls)
```

你会不会感觉特别卡你你会不会感觉特别卡，欸现在为啥又不卡了？？你好啊现在还有点卡还是有点卡还是有点卡还是有点卡

你好现在还卡吗，我想知道现在还卡吗
现在还卡吗现在不卡了，开启源代码模式就不卡了确实是的开启源代码模式他就好多了不怎么卡了

现在还觉得卡吗现在还卡么

现在还卡吗现在还卡吗

为什么这样就很卡呢

现在还是卡吗现在还是很卡吗现在还是有点卡

### 9月22日

从头开始复习

#### input函数

用于从控制台获得用户输入，无论输入什么，它都以字符串类型返回结果，它还可以包含一些提示性文字提醒用户。

`<变量>input(<输入提示性文字>)`

#### eval函数

用于去掉字符串最外层的引号，并按照python语句的执行方式执行其中的字符内容

例如

```python
a=eval("1.2")
print(a)
结果是
1.2

a=eval("1.2+3.4")
print(a)
结果是
4.6
```

注：eval只会去掉最外面的一对引号
例如在处理`"'pybook'"`的时候他就只会去掉最外面的，'pybook'被解释为字符串

### 9月23日

最后的挣扎

今天晚上看了基本数据类型

复习了字典的使用方法

```python
#字典
zidian = {1:'你',2:'好'}
print(zidian)
print(zidian[1])
print(zidian.keys())
print(zidian.values())
```

创建空字典：

```python
zidian = {}
```

dict()是一个字典的构造函数，用法如下

```python
>>>dict([('Runoob', 1), ('Google', 2), ('Taobao', 3)])
>>>{'Runoob': 1, 'Google': 2, 'Taobao': 3}
```

当然也可以不用dict()来构造，直接a={xx:xx,xx:xx}就可以

#### 类型转换

分为隐式类型转换和显性类型转换

显性类型转换可以用下表的内置函数

| 函数                                                         | 描述                                                |
| ------------------------------------------------------------ | --------------------------------------------------- |
| int(x [,base\])                                              | 将x转换为一个整数                                   |
| float(x)                                                     | 将x转换到一个浮点数                                 |
| complex(real[,imag\])                                        | 创建一个复数                                        |
| str(x)                                                       | 将对象 x 转换为字符串                               |
| repr(x)                                                      | 将对象 x 转换为表达式字符串                         |
| eval(str)                                                    | 用来计算在字符串中的有效Python表达式,并返回一个对象 |
| tuple(s)                                                     | 将序列 s 转换为一个元组                             |
| [list(s)](https://www.runoob.com/python3/python3-att-list-list.html) | 将序列 s 转换为一个列表                             |
| [set(s)](https://www.runoob.com/python3/python-func-set.html) | 转换为可变集合                                      |
| [dict(d)](https://www.runoob.com/python3/python-func-dict.html) | 创建一个字典。d 必须是一个 (key, value)元组序列。   |
| [frozenset(s)](https://www.runoob.com/python3/python-func-frozenset.html) | 转换为不可变集合                                    |
| [chr(x)](https://www.runoob.com/python3/python-func-chr.html) | 将一个整数转换为一个字符                            |
| [ord(x)](https://www.runoob.com/python3/python-func-ord.html) | 将一个字符转换为它的整数值                          |
| [hex(x)](https://www.runoob.com/python3/python-func-hex.html) | 将一个整数转换为一个十六进制字符串                  |
| [oct(x)](https://www.runoob.com/python3/python-func-oct.html) | 将一个整数转换为一个八进制字符串                    |

#### 字符串更新


你可以截取字符串的一部分并与其他字段拼接，如下实例：
实例(Python 3.0+)
```python
#!/usr/bin/python3
 
var1 = 'Hello World!'
 
print ("已更新字符串 : ", var1[:6] + 'Runoob!')
```
以上实例执行结果

已更新字符串 :  Hello Runoob!

还有好多的字符串函数

## 9月24日

我今天下午考试，虽然睡到9点多才起来，但是也要最后挣扎一下啊

### 列表

append()方法：用于在列表后面加元素

```python
list1.append('Baidu')
```

list(seq)函数：用于将元组转换为列表

###  元组

```python
>>> tup1 = (50)
>>> type(tup1)     # 不加逗号，类型为整型
<class 'int'>

>>> tup1 = (50,)
>>> type(tup1)     # 加上逗号，类型为元组
<class 'tuple'>
```

创建空元组

```python
tup1 = ()
```



tuple(iterable) 将可迭代系列转换为元组。

`>>> list1= ['Google', 'Taobao', 'Runoob', 'Baidu'] `

`>>> tuple1=tuple(list1) `

`>>> tuple1 ('Google', 'Taobao', 'Runoob', 'Baidu')` 
