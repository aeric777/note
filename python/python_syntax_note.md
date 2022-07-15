# Python Note

> 2021.11.22

## 概括
    Python属于解释型语言，其底层仍然使用C进行编译。其本质上是为了扩大受众群体，提高编程效率而开发的语言，其高度抽象的特点使其更加易读，高度封装使其更加容易使用。(注：本文使用**Linux**平台进行编程)

#### 解释器
    基于不同的适用平台和编译语言，Python可以使用多种不同的解释器，其中常用的是`CPython`, `IPython`, `PyPy`等。

#### 动态语言
    使用前不需要声明变量类型。


------------------
## 第一个Python程序
#### 执行`Python`程序 & 交互模式
- 在终端输入 `python3` 调用 **交互模式**，出现`>>>`提示符，并且打印出每一步的结果
- 执行`.py`文件执行python程序，只显示最终结果，不会逐步打印结果。

#### 编辑`Python`程序
    本文使用`Vim`进行编辑，运行方法：
- 在命令行中输入
```
python3 filename.py
```
- 在文件开头添加`#!usr/bin/env python3`后，命令行中输入
```
chmod a+x filename.py
```
为文件添加运行权限后，便可以直接运行(仅在`Linux`, `Mac`系统有效)
```
filename.py
```

------------------
## **Python**数据类型

#### 字符串编码
    在计算机内存中，统一使用`Unicode`编码，当需要保存到硬盘或者需要传输的时候，就转换为`UTF-8`编码。用记事本编辑的时候，从文件读取的`UTF-8`字符被转换为`Unicode`字符到内存里，编辑完成后，保存的时候再把`Unicode`转换为`UTF-8`保存到文件.
    Python3中的字符串以`Unicode`进行编码。
    通常在Python程序开头写上：
```
#!/usr/bin/env python3      //这是一个使用Python3编译的程序
# -*- coding: utf-8 -*-     //按照UTF-8编码读取源代码
```

#### 整数
- 可表示任意大小的整数
- 可用十六进制表示，以`0x`开头
- 可使用`_`分割，不影响数值(`1_000_000 == 1000000`)

#### 浮点数

### 字符串
- 使用`""`,` '' `进行标识
- 中间可使用转义字符串
- Python还允许用`r''`表示` '' `内部的字符串默认不转义
- Python允许用` '''...''' `的格式表示多行内容,示例代码：
```python
>>> print('''line1
... line2
... line3''')
```
输出结果：
```
line1
line2
line3
```

#### Bytes
    Python对`bytes`类型的数据用带b前缀的单引号或双引号(`b`` `)表示;

- 以`Unicode`表示的`str`通过`encode()`方法可以编码为指定的`bytes`类型：
```
>>> 'ABC'.encode('ascii')
b'ABC'

>>> '中文'.encode('utf-8')
b'\xe4\xb8\xad\xe6\x96\x87'

>>> '中文'.encode('ascii')      //中文编码的范围超过了ASCII编码的范围，Python会报错。
Traceback (most recent call last):
    File "<stdin>", line 1, in <module>
UnicodeEncodeError: 'ascii' codec can't encode characters in position 0-1: ordinal not in range(128)
```

- 将`bytes`(通常是网络或磁盘上读取的**字节流**)变为`str`，需要使用`decode()`:

#### 布尔值
`True`,`False`

#### 逻辑运算
`and`,`or`, `not`

#### 空值
`None`

#### 常量
- Python无常量保护机制`const`
- 通常使用约定俗成的大写表示常量

#### 除法
- 浮点除法`/`
```
>>> 10 / 3
3.3333333333333335
>>> 9 / 3
3.0(整数结果表示为浮点数)
```
- 地板除法`//`
```
>>> 10 // 3
3
```


------------------
## **Python**函数
```
注释使用`#`
通常来讲每一行都是一个语句，但是当语句以冒号`:`结尾时，缩进的语句视为代码块。
```
1.`print`
```
print("argument1","argument2"...)`
```
- 接受多个变量（enclosed with `""` or ` `` `）,中间使用`,`隔开。注意输出时`,`会输出为**空格**.
- 使用`%`进行格式化
| 格式化字符        |对应           |
| --------          |:-----:        |
| %d                |整数           |
| %f                |浮点数         |
| %s                |字符串         |
|%x                 |十六进制整数   |

- 也可以使用`format()`,`f-string`方法进行格式化。

2.`input`
```
variable=input()
```
- 提示将信息输入至variable

3.`ord()`获取字符的整数表示, `chr()`将编码转换为对应的字符

4.`encode()` & `decode()`进行`bytes` , `str`之间的转换

5.`len()`计算字符长度
```
PS: 对于str计算字符数；对于bytes计算字节数
>>> len(b'ABC')     //一个英文字符占一个Bytes字节
3

>>> len('中文'.encode('utf-8'))     //中文字符占3个
6
```