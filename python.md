## Pyhton-排序

```python
# 这是一个示例 Python 脚本。

# 按 Shift+F10 执行或将其替换为您的代码。
# 按 双击 Shift 在所有地方搜索类、文件、工具窗口、操作和设置。

stus = [{'name': 'zs', 'height': '1.9m', 'weight': 60, 'scores': [110, 90, 80]},
        {'name': 'zsf', 'height': '150cm', 'weight': 75, 'scores': [130, 90, 80]},
        {'name': 'sb', 'height': '180CM', 'weight': 70, 'scores': [120, 90, 80]},
        ]


# def weight_sort(item):
#     return -item['weight']

# todo 按照体重排序
# stus.sort(key=weight_sort)

# todo 按照学习成绩的总和排序
# stus.sort(key=lambda score: sum(score['scores']))

# todo 按照身高排序
def height_sort(item):
    height_str = item['height']
    height_str = height_str.lower()
    # 区分m和cm
    height=0
    # endswith()查看字符串是否为cm结尾的函数
    if height_str.endswith('cm'):
        height_str = height_str.replace('cm', '')
        height = int(height_str) / 100
    else:
        height_str = height_str.replace('m', '')
        height = float(height_str)
    return height


stus.sort(key=height_sort)

for stu in stus:
    print(stu)

```



get()函数的声明如下:

```python
1 get(ur1，params=None，headers=None，cookies=None, verify=True,proxies=None，timeout=None，**kwargs)
```

- url:**必选**，表示**请求的URL**。
- params:可选，表示请求的**查询字符串**。
- headers:可选，表示请求的**请求头**，该参数只支持**字典**类型的值。
- cookies:可选，表示**请求的Cookie信息**，该参数支持字典或
- verify:可选，表示是否启用**SSL证书**，默认值为True。
- proxies:可选，用于**设置代理服务器**，该参数只支持字典类型的值。
- timeout:可选，表示请求网页时**设定的超时时长**，以秒为单位。



## SSL证书验证

**SSL证书**是一种数字证书，类似于驾驶证、护照和营业执照的电子副本。由受信任的数字证书颁发机构CA在验证服务器身份后颁发，具有服务器身份验证和数据传输加密功能。

当使用Requests调用请求函数发送请求时，由于请求函数的verify参数的默认值为True，所以每次请求网站时默认都会进行SSL证书的验证。

不过，有些网站可能没有购买SSL证书，或者SSL证书失效，当程序访问这类网站时会因为找不到SSL证书而抛出SSLError是堂。



## 代理服务

- **高度匿名代理服务器**

​	会将数据包原封不动地转发给服务器，让服务器认为当前访问的用户只是一个普通客户端，而不是代理服务器，并记录代理服务器的IP地址。

- **普通匿名代理服务器**

​	会对数据包进行一些改动，服务器可能会发现当前访问的用户是代理服务器，也可能会追查到客户端的真实IP地址。

- **透明代理服务器**

​	不仅会改动数据包，还会暴露当前访问客户端的真实lP地址。

## 正则表达式

| 正则表达式 | 匹配字符   | 备注                                                         |
| ---------- | ---------- | ------------------------------------------------------------ |
| \d         | 数字       | digit首字母，表示一个数字                                    |
| \D         | 一个非数字 |                                                              |
| \w         | 单词字符   | word首字母,表示一个单词字符，可以是:26个英文字母的大小写或数字下划线_ |
| \W         | 非单词字符 |                                                              |
| \s         | 空白字符   | space首字母，表示一个空白字符，可以是:空格、换行(\n)、回车(\r)、制表符(Nt) |
| \S         | 非空白字符 |                                                              |
| .          | 任意字符   | 在默认模式，匹配除了换行的任意字符。如果指定了标签DOTALL,它将匹配包括换行符的任意字符 |



| 量词  | 含义                                        | 举例      | 说明                                                       |
| ----- | ------------------------------------------- | --------- | ---------------------------------------------------------- |
| ?     | 对它前面的正则式，匹配0次或1次，等价于{0,1} | a\d?      | 表示a后面跟0个或者1个数字                                  |
| +     | 对它前面的正则式，匹配1次或多次，等价于{1,} | py+       | 表示p后面跟了至少1个y的字符串                              |
| *     | 对它前面的正则式，匹配0次或多次，等价于{0,} | .*        | 正则表达式里常见写法，表示任意字符串(不考虑换行符的情况下) |
| {m}   | 对其之前的正则式，匹配 m次                  | \d{5}     | 表示5个数字的字符串                                        |
| {m,}  | 对其之前的正则式，匹配至少m次               | \d{5,}    | 表示至少5个数字的字符串                                    |
| {m,n} | 对其之前的正则式，匹配m~n次                 | 0\d{2,3}: | 表示数字0后跟有2至3个数字                                  |

```正则表达式
\d{3,4}-\d{7,}|\(\d{3,4}\)\d{7,}
(全段匹配 \d表示数字 {表示数字范围} 后面跟-表示匹配-部分)

0991-8585671
023-58102054
(0991)8585617
(023)58102054
```



## XPath语法

### 1. 选取节点

**常见路径表达式**

| 表达式 | 说明                                 |
| ------ | ------------------------------------ |
| 点名称 | 选取此节点的所有子节点?              |
| /      | 从当前节点选择直接子节点             |
| //     | 从当前节点选择子孙节点，忽略层级关系 |
| .      | 选取当前节点                         |
| ..     | 选取当前节点的父节点                 |
| @      | 选取属性节点                         |

**常见的XPath函数**

| 函数                      | 说明                                            |
| ------------------------- | ----------------------------------------------- |
| position()数字比较        | 返回当前被处理的节点的位置                      |
| last()                    | 返回当前节点集中的最后一个节点                  |
| count()                   | 返回节点的总数目                                |
| max((arg,arg..))          | 返回大于其他参数的参数                          |
| min((arg,arg…))           | 返回小于其他参数的参数                          |
| name()                    | 返回当前节点的名称                              |
| current-date()            | 返回当前的日期（带有时区)                       |
| current-time()            | 返回当前的时间(带有时区)                        |
| contains(string1,string2) | 若string1包含string2，则返回true，否则返回false |

### 2.从字符串或文件中解析XML

#### 2.1.解析函数

- **fromstring()函数:**
  - 从字符串中解析XML文档或片段，返回根节点(或解析器目标返回的结果)。
  - 通常用于将XML字面量直接写入到源代码中
- **XML()函数:**
  - 从字符串中解析XML文档或片段，返回根节点(或解析器目标返回的结果)。
  - XML方法，与fromstring方法基本一样
- **HTML()函数:**
  - 从字符串常量中解析HTML文档或片段，并能够自动补全文档或片段中缺少的<htm1>和<body>元素。
- **parse()函数:**
  - 从XML文件中直接解析









# Selenium
