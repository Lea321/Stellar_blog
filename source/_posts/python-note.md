---
title: Python笔记
tags:
  - 笔记
categories: 学习笔记
cover: https://cdn.leonus.cn/cover/python.webp
date: 2021-10-30 10:53:39
updated: 2021-10-30 10:53:39
poster: 
  topic: 学习笔记
  headline: Python笔记
  caption: 
  color:
---
## 基础知识

### 匿名函数lambda

```python
name = lambda 参数 : 表达式
```

### 字符串String

```python
# Python支持原始字符串，字符串前面加上 `r` 即可（输入什么显示什么,注意引号）
a = r'print("\")'
print(a)
# 输出结果：print("\")
s.isdigit() #检测字符串是否只由数字组成
s.isupper() #检测字符串中所有的字母是否都为大写
s.islower() #检测字符串中所有的字母是否都为小写
```

### 字符串切片

```python
# sname[start:end:step]
s = "hello world"
print(s[0::2])
# 结果：hlowrd
```

### 列表List
```python
list = [1,2,3,4,5]

#列表推导式
ls = [i for i in range(20)] #[0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19]

ls.sort(key,reverse=True) #按降序排序
```

### 元组Tuple
```python
tuple = (1,2,3,4)

# 元组和列表非常相似，都可存放多个数据，可存放不同数据类型的数据
# 不同点：
# 列表使用 [] 定义，元组使用 () 定义
# 列表中数据可修改，元组中数据不能修改

# 定义空元组(没有意义，因为元组不可修改)
tuple1 = ()
tuple2 = tuple()
# 定义一个数据元素的元组
tuple3 = (1,)
# 不能是 tuple3 = (1)，这样是一个int类型
```


### 字典Dictionary

```python
dict1 = {key1:value1,key2:value2, ...}
# 字典的key 可以是 字符串类型和数字类型（int float），不能是列表

# 定义空字典
dict2 = {}
dict3 = dict()
# 字典中没有下标的概念，通过key值访问对应的value值

# 如果key值不存在
# print(dict1['key']) #代码报错
# dict1.get(key) 不会报错,返回none

s = {'a':1,'b':2,'c':3}
s.items() #('a', 1),('b', 2),('c', 3)
s,keys() #a,b,c
s.values() #1,2,3
s.get(key,default) #查找key，有的话返回值，没有返回default。
```




## 常用函数
```python
bin(number)  # 转二进制
oct(number)  # 转八进制
hex(number)  # 转十六进制
len(x)  # 字符串x长度
chr(x)  # 返回Unicode编码x对应的字符
ord(x)  # 返回字符x对应的Unicode编码
```



## 常用模块和库

### os
```python
import os

os.getcwd() #当前目录
os.listdir() #返回指定目录下的所有文件和目录名
os.remove() #删除一个文件
os.path.isfile() #检测给出的路径是否是一个文件
os.path.isdir() #检测给出的路径是否是一个目录
os.path.exists() #检测给出的路径是否存在
os.path.dirname() #获取路径名
os.path.abspath() #获取绝对路径
os.path.basename() #获取文件名
os.system() #运行shell命令
os.rename(old,new) #重命名
os.removedirs() #删除多级目录
os.makedirs() #创建多级目录
os.mkdir() #创建目录
```

### time
```python
import time

time.time() #获取时间戳
time.localtime()  # 将一个时间戳转换为当前时区的struct_time，参数可为空
time.gmtime() #将一个时间戳转换成UTC时区的struct_time
time.mktime() #将一个struct_time转成时间戳
time.sleep(n) #推迟n秒
time.strftime("%Y-%m-%d %H:%M:%S") #格式化时间,可添加指定参数struct_time，默认time.localtime()
time.strptime() #把一个格式化时间转成struct_time，和time.strftime()是逆操作

```

### datetime
```python
import datetime

datetime.date #表示日期的类
datetime.time #表示时间的类
datetime.datetime #表示日期时间
datetime.timedelta # 表示时间间隔，即两个时间点之间的长度
datetime.tzinfo #与时区有关的相关信息
datetime.datetime.now() #2022-06-03 15:23:01.394036
datetime.date.fromtimestamp() #将一个时间戳转成date日期类型
```

### random

```python
random.choices(demo, k=n)  # 放回抽样选取
random.sample(demo, n)  # 不放回抽样选取
```


### turtle

```python
turtle.seth() # 函数角度的方向
turtle.tracer(False) # 图形将一次性画好
```

### jieba

```python
jieba.cut(str) # 返回可迭代的数据类型
jieba.lcut(str) # 返回一个列表类型，建议使用
```

> 参考文档：[https://www.cnblogs.com/wkfvawl/p/9487165.html](https://www.cnblogs.com/wkfvawl/p/9487165.html)


### wordcloud

```python
w=wordcloud.WordCloud(font_path="C:\\Windows\\Fonts\\msyh.ttf") # 创建对象，设置图片样式
w.generate(str) # str：用空格隔开的字符串
w.to_file("demo.png") # 保存图片
```

> 参考文档：https://www.cnblogs.com/dadazunzhe/p/11215452.html

### tkinter

```python
# 空间优先级别为：界面空间 > 前辈组件独占空间 > 后辈组件独占空间 > 前辈组件可扩展空间 > 后辈组件可扩展空间

win.geometry('800x500')
win.geometry('+560+250')
win.title('富贵论坛自动评论-v0.1')

Entry.get()
Text.get('1.0',END) #1.0表示第一行第一列
Entry.insert('insert','内容') # 插入内容，Text通用
```

> 参考文档：
>
> https://blog.csdn.net/qq_46018418/article/details/105927203
>
> https://blog.csdn.net/superfanstoprogram/article/details/83713196
>
> https://www.runoob.com/python/python-gui-tkinter.html



### selenium

```python
from selenium import wedriver
wb = webdriver.Chrome()
wb.get('url')
wb.implicitly_wait(10) # 10秒内没找到元素报错
wb.delete_all_cookies() # 删除所有cookies
wb.refresh() # 刷新

# 获取cookies
c = wb.get_cookies()
print(c)

# 添加cookies
for item in cookies:
    if 'expiry' in cookies:
        del cookies['expiry']
    browser.add_cookie(item)
    
# 下滑到底部
wb.execute_script("window.scrollTo(0, document.body.scrollHeight);")

# 输入内容
browser.find_element_by_xpath('xpath语法').send_keys('内容')

# 获取标签文本
text = browser.find_element_by_xpath('xpath语法').get_attribute('textContent')
```

> 参考文档：
>
> https://zhuanlan.zhihu.com/p/111859925
>



## 爬虫笔记

### 常用模块和方法

```python
import requests #get post 超时使用属性timeout=2
import re #findall(正则表达式，内容)
import time
import os
import lxml #etree
import jsom
import js2py
import jsonpath #jsonpath
from fake_useragent import UserAgent #UserAgent().random
import pymysql
import hashlib
import moviepy.editor
```

## 小细节

```python
切片s[:2] # 不包含2
randint[1:100] # 包含100
range(10) # 不包含10
```

