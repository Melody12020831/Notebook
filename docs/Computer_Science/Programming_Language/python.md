---
statistics: True
comments: true
---

# Python

!!! Abstract
    这是我在学习 "CS50P Introduction to Programming with Python" 时所做的笔记 ([这里指路B站链接🔗](https://www.bilibili.com/video/BV1z5411X7wX/?vd_source=5c63e6e26ff6071f4e69839b18529555)) ，难免不全。笔者之后有计划继续进一步学习python，因此仍会更新。

## print and main
```python
print(*objects, sep=' ', end='\n', file=sys.stdout, flush=False)
```

- print函数：输出多个对象，并且可以自定义分隔符、结束符等

```python
print(f"Hello, your name is {name}!")
```

- 格式化字符串：将变量插入字符串中，使用f开头，大括号中插入变量名

```python
if __name__ == "__main__":
```

- 判断当前脚本是否为主程序执行

---

## change string

```python
str.strip([chars])

#e.g.
name = name.strip()
```

- chars（可选）：指定要移除的字符集，如果不指定，则默认移除空白字符。

```python
name = name.capitalize()
```

- 将字符串的首字母大写

```python
name = name.upper()
```

- 将字符串全部转换为大写

```python
name = name.lower()
```

- 将字符串全部转换为小写

```python
name = name.title()
```
- 将字符串的每个单词首字母大写

```python
str.split(separator, maxsplit)

# e.g.
name = name.split('')
```

- 按指定字符拆分字符串，返回列表。

- separator（可选）：指定分隔符，如果不指定，任何空白字符（空格、制表符、换行符等）都会被视为分隔符。

- maxsplit（可选）：指定最大拆分次数，分割后的子字符串数量不会超过 maxsplit。如果不指定，则分割所有可能的地方。

## print numbers

```python
print(f"{z:,}")
```

- 格式化输出数字，添加千位分隔符。

- 例如，如果z的值是1234567，那么格式化后的字符串将是"1,234,567"。

```python
print(f"{z:.2f}")
```

- 格式化输出数字，保留两位小数

```python
print(f"{z:,.2f}")
```

- 格式化输出数字，添加千位分隔符并保留两位小数

```python
round(number[, ndigits])
```

- 对数字进行四舍五入。

- number：需要四舍五入的数字。

- ndigits（可选）：指定小数点后保留的位数。如果不提供这个参数，函数将返回最接近的整数。

---

## match

```python
match name:
    case "Alice":
        print("Hello, Alice!")
    case "Bob":
        print("Hello, Bob!")
    case _:
        print("Hello, stranger!")
```

- 有点类似 C 里面的 `switch-case` 语句

---

## random

!!! Info
    要使用以下函数，需要 `import random`

```python
number = random.randint(1, 10)
```

- 生成一个1到10之间的随机整数

```python
number = random.random()
```

- 生成一个0到1之间的随机浮点数

```python
number = random.uniform(1, 10)
```

- 生成一个1到10之间的随机浮点数

```python
choice = random.choice(["apple", "banana", "cherry"])
```

- 从列表中随机选择一个元素

```python
random.shuffle(my_list)
```

- 随机打乱列表中的元素

---

## statistics

!!! Info
    要使用以下函数，需要 `import statistics`

```python
mean = statistics.mean(my_list)
```

- 计算列表中元素的均值

```python
median = statistics.median(my_list)
```

- 计算列表中元素的中位数

```python
mode = statistics.mode(my_list)
```

- 计算列表中元素的众数

```python
std_dev = statistics.stdev(my_list)
```

- 计算列表中元素的标准差

---

## sys

!!! Info
    要使用以下函数，需要 `import sys`

- `sys`：用于与Python解释器交互，提供命令行参数处理、程序退出等功能。

```python
print(sys.argv)
```

- 输出命令行参数

```python
print(sys.argv[0])
```

- 输出第一个命令行参数，通常是脚本名称

```python
print(sys.argv[1:-1])
```

- 输出命令行参数中的中间部分

```python
sys.exit("Exiting the program")
```

- 退出程序，并输出指定的消息

---

## cowsay

!!! Info
    要使用以下函数，需要 `import cowsay`

```python
cowsay.cow("Hello, world!")
```

- 使用cowsay打印一个牛说的“Hello, world!”

```python
cowsay.trex("Hello, world!")
```

- 使用cowsay打印一个恐龙说的“Hello, world!”

---

## requests and json

!!! Info
    要使用以下函数，需要 `import requests` 和 `import json`

```python
response = requests.get("https://www.google.com")
```

- requests.get 方法通过构造一个 HTTP GET 请求，向指定的 URL 发送请求，并返回一个 Response 对象。这个对象包含了服务器响应的所有信息，如状态码、响应头、响应体等。

```python
print(response.status_code)
```

- 打印响应的状态码

!!! note
    在HTTP协议中，状态码是一个三位数的整数，用于表示服务器对请求的处理结果。状态码分为五大类，分别是：

    1. 1xx（信息性状态码）：表示请求已接收，继续处理。

    2. 2xx（成功状态码）：表示请求已成功接收、理解和接受。

    3. 3xx（重定向状态码）：表示需要客户端采取进一步操作才能完成请求。

    4. 4xx（客户端错误状态码）：表示请求包含语法错误或无法被执行。

    5. 5xx（服务器错误状态码）：表示服务器在处理请求的过程中发生了错误。

```python
print(response.content)
```

- 打印响应的内容。上述的 `response.content` 是HTTP响应对象的一个属性，它包含了服务器返回的实际内容。这个内容是以字节形式存储的。

```python
print(response.headers)
```

- 打印响应的头部信息。上述的 `response.headers` 是HTTP响应对象的一个属性，它包含了服务器返回的所有头部信息。这些信息是以字典形式存储的，可以通过键值对的方式访问。

!!! note
    HTTP头部信息是HTTP协议的一部分，用于在客户端和服务器之间传递额外的信息。这些信息包括请求和响应的元数据，如内容类型、内容长度、服务器类型等。

```python
print(response.json())
```

- 打印响应的JSON数据，`.json()` 方法将响应的内容解析为Python的字典或列表，具体取决于JSON数据的结构。

```python
print(json.dumps(response.json(), indent=4))
```

- `json.dumps` 函数将Python对象转换为JSON格式的字符串。

- `indent=4` 参数指定了输出的字符串应该使用4个空格进行缩进，使得输出的JSON字符串更加易读。

---

## assert

```python
assert 1 == 2, "1 is not equal to 2"
```

- 断言1等于2，如果不等则抛出异常并打印消息。

!!! Info
    `assert` 语句通常用于开发和测试阶段，用于检查代码中的假设是否成立。如果假设不成立，程序会立即停止执行，并给出错误信息，帮助开发者快速定位问题。

---

## file I/O

```python
with open("file.txt", "w") as f:
    f.write("Hello, world!")
```

- 写入文件（会覆盖原文件内容）

```python
with open("file.txt", "a") as f:
    f.write("Hello, world!")

    # or
    name = input("Enter your name: ")
    f.write(f"{name}\n")
```

- 写入文件（会追加内容到文件末尾）

```python
with open("file.txt", "r") as f:
    content = f.readlines()

    # or
    for line in f:
        print(line, end="")

        # or 去除每行末尾的换行符
        print(line,rstrip())

```

- 读取文件内容

```python
with open("file.txt") as f:
    for line in sorted(f):
        print(line, end="")
```

- 排序文件中的内容

- `sorted(iterable, key=None, reverse=False)`
    - `iterable` ：要排序的可迭代对象，如列表、元组、字典等。
    - `key`：一个函数，用于从每个元素中提取比较键。默认为 None，表示直接对元素进行排序。
    - `reverse`：如果设置为 True ，则降序排序。如果设置为  False ，则列表元素将被升序排序。默认为 False 。

!!! note "further for key"
    `key` 可以是一个函数，也可以是一个可调用对象。如果 `key` 是一个函数，那么它将被应用于每个元素，并返回一个用于排序的键。如果 `key` 是一个可调用对象，那么它将被应用于每个元素，并返回一个用于排序的键。

    - 如果 `key` 是一个函数，那么它将被应用于每个元素，并返回一个用于排序的键。例如，如果 `key` 是一个函数，它接受一个字符串作为参数，并返回字符串的长度，那么 `sorted` 函数将根据字符串的长度对字符串进行排序。

    - 如果 `key` 是一个可调用对象，那么它将被应用于每个元素，并返回一个用于排序的键。例如，`sorted_people = sorted(people, key=lambda person: person["age"])` 将根据每个人的年龄对 `people` 列表进行排序。

    这个 `lambda` 函数是一个匿名函数。 `lambda arguments: expression` 。

        - `arguments` : 是一个或多个参数，用逗号分隔。
        - `expression` : 函数的表达式，这个表达式的结果就是函数的返回值。

!!! note
    `with` 语句用于管理文件的上下文，当 `with` 语句块结束时，无论是否发生异常，文件对象都会被正确关闭。

---

## csv

!!! Info
    要使用以下函数，需要 `import csv` 。

!!! note
    `csv` 模块用于读写 CSV（Comma-Separated Values，逗号分隔值）文件。CSV 文件是一种常见的文本文件格式，用于存储表格数据。每行数据由多个字段组成，字段之间用逗号分隔。

```python
with open("file.csv", "r") as f:
    reader = csv.reader(f)
    for row in reader:
        print(row[0])
```

- 读取CSV文件，自动识别分隔符

```python
reader = csv.DictReader(f)
for row in reader:
    print(row["name"])
```

- 读取CSV文件，第一行是列名

```python
with open("file.csv", "a", newline="") as f:
    writer = csv.writer(f)
    writer.writerow(["Name", "Age", "City"])
```

- 写入CSV文件，指定列名

## re

!!! Info
    要使用以下函数，需要 `import re` 。

!!! note
    `re` 模块用于在字符串中搜索和替换模式。它提供了正则表达式操作的各种函数，如搜索、匹配、替换等。

```python
re.search(pattern, string, flags=0)
```

- 用于在给定的字符串中搜索与正则表达式模式匹配的第一个位置。如果找到匹配项，则返回一个匹配对象；如果没有找到匹配项，则返回 None。

- `pattern` : 正则表达式模式，用于匹配字符串中的内容。

- `string` : 要搜索的字符串。

- `flags` : 可选参数，用于修改正则表达式的匹配行为。默认值为 0，表示不使用任何标志。

??? note "about pattern"
    "." 匹配除换行符以外的任意字符
    "^" 匹配字符串的开头
    "$" 匹配字符串的结尾
    "*" 匹配前面的子表达式零次或多次
    "+" 匹配前面的子表达式一次或多次
    "?" 匹配前面的子表达式零次或一次
    "{n}" 匹配前面的子表达式n次
    "{n,}" 匹配前面的子表达式至少n次
    "{n,m}" 匹配前面的子表达式至少n次,至多m次
    "[...]" 匹配方括号内的任意一个字符
    "[^...]" 匹配不在方括号内的任意一个字符
    "\d" 匹配一个数字字符
    "\D" 匹配一个非数字字符
    "\s" 匹配一个空白字符
    "\S" 匹配一个非空白字符
    "\w" 匹配一个字母或数字字符
    "\W" 匹配一个非字母或数字字符
    "(A|B)" 匹配A或B
    "()" 匹配括号内的表达式

??? note "about flags"
    `re.I` | `re.IGNORECASE` 忽略大小写
    
    `re.M` | `re.MULTILINE` 多行模式,改变 `^` 和 `$` 的行为, `^` 和 `$` 可以匹配每行的开始和结束）
    
    `re.S` 默认情况下，`.` 字符在正则表达式中匹配除换行符以外的任何字符。使用 `re.S` | `re.DOTALL` 可使 `.` 字符将匹配任何字符，包括换行符。

### example

```python
    email = input("Enter your email: ").strip()
    re.research(r".+@.+\.edu",email)
```

- `r` 表示字符串是原始字符串，不会对反斜杠进行转义，也即不需要解释器再次进行转义。

- `\.edu` 表示匹配字符 `.edu` 。由于 `.` 在正则表达式中是一个特殊字符，表示任意字符，所以需要用 `\` 进行转义，表示匹配字符 `.` 。

- 这段代码的用途是检查一个给定的电子邮件地址是否包含 `@` 符号，并且域名部分是否以 `.edu` 结尾。

---

```python
matches = re.research(r"^(.+), (.+)$", name)
if matches:
    last, first = matches.groups()
print(f"Last name: {last}, First name: {first}")

# or
if matches:
    last = matches.group(1) 
    first = matches.group(2)
print(f"Last name: {last}, First name: {first}")
```

- `^` 匹配字符串的开始位置

- `(.+)` 匹配一个或多个任意字符，并将其捕获为一个组

- `, ` 匹配一个逗号和一个空格

- `(.+)` 匹配一个或多个任意字符，并将其捕获为另一个组

- `$` 匹配字符串的结束位置

- `matches.groups()` 返回一个包含所有捕获组的元组，元组中的每个元素对应于一个捕获组。在这个例子中，`matches.groups()` 返回一个包含两个元素的元组，第一个元素是 `last`，第二个元素是 `first`。

---

```python
url = input("Enter URL: ").strip()

username = url.replace("http://", "")
# or
username = url.removeprefix("http://")

username = re.sub(r"^(https?://)?(www\.)?twitter\.com/", "", url)

# attention: group(0) is the whole match and group(1) is the first group (www\.)
matches = re.search(r"https?://(www\.)?twitter\.com/(.+)", url,re.IGNORECASE).group(2)
```

- 找出 `url` 中的 `twitter` 用户名，忽略大小写

!!! note
    `re.sub(pattern, repl, string, count=0, flags=0)`

    - `pattern` ：正则表达式模式，用于匹配要替换的子串。

    - `repl` ：替换字符串，用于替换匹配到的子串。

    - `string` ：要搜索和替换的原始字符串。

    - `count` ：可选参数，指定替换的最大次数。默认为 0，表示替换所有匹配的子串。

    - `flags` ：可选参数，用于修改正则表达式的匹配行为。例如，`re.IGNORECASE` 表示忽略大小写。

---

## class

!!! Info
    还没整理完，待续。估计会等到 cpp 整理完再整理。(咕咕咕)

```python
class Student:
    def __init__(self, name, house=None):
        # 如果 house 没有传入值，则默认为 None

        if not name:
            raise ValueError("Name is required")
        self.name = name
        self.house = house

    def __str__(self):
        return f"{self.name} from {self.house}"

    @property
    def house(self):
        return self._house

    @house.setter
    def house(self, value):
        if not value:
            raise ValueError("House is required")
        self._house = value
```

## set

```python
numbers = {1, 2, 3, 4}
```

- 创建集合，如果集合中有重复的元素，则只会保留一个。

!!! note
    集合是无序的，不能通过索引访问元素。集合的元素必须是不可变类型（如整数、浮点数、字符串、元组等），不能是列表、字典或集合等可变类型。

```python
numbers.add(5)
numbers.remove(3)
```

- `add()` 方法用于向集合中添加元素。

- `remove()` 方法用于从集合中删除元素。如果元素不存在，则会引发 `KeyError` 异常。

```python
numbers1 = {1, 2, 3}
numbers2 = {2, 3, 4}

intersection = numbers1 & numbers2
union = numbers1 | numbers2
difference = numbers1 - numbers2
```

- `&` 运算符用于计算两个集合的交集。

- `|` 运算符用于计算两个集合的并集。

- `-` 运算符用于计算两个集合的差集。

---

## argparse

!!! Info
    要使用以下函数，需要 `import argparse`。

```python
parser = argparse.ArgumentParser(description="这是一个示例脚本")
```

- 创建ArgumentParser对象

```python
parser.add_argument('input_file', type=str, help='输入文件的路径')
parser.add_argument('-o', '--output_file', type=str, default='output.txt', help='输出文件的路径')
parser.add_argument('-n', '--number', type=int, default=10, help='要处理的数量')
```

- 添加参数，`add_argument()` 方法用于添加命令行参数。参数的名称、类型和默认值都可以指定。

```python
args = parser.parse_args()
```

- 解析命令行参数，将结果存储在 `args` 对象中。

```python
print(f"Name: {args.name}, Age: {args.age}")
```

- 使用 `args` 对象的属性访问命令行参数的值，并打印出来。

---

???+ note "example"
    ```python
    import argparse

    parser = argparse.ArgumentParser(description="这是一个示例脚本")

    parser.add_argument('input_file', type=str, help='输入文件的路径')

    parser.add_argument('-o', '--output_file', type=str, default='output.txt', help='输出文件的路径')

    parser.add_argument('-n', '--number', type=int, default=10, help='要处理的数量')

    args = parser.parse_args()

    print(f"Name: {args.name}, Age: {args.age}")
    ```

??? note "output"
    ```shell
    $ python example.py input.txt -o output.txt -n 5
    ```

    输入文件: input.txt
    
    输出文件: output.txt
    
    数量: 5

??? Info "you can see them by typing --help"
    ```shell
    $ python example.py --help
    ```

    此时会出现

    ```python
    usage: your_script.py [-h] [-o OUTPUT_FILE] [-n NUMBER] input_file

    这是一个示例脚本

    positional arguments:
    input_file            输入文件的路径

    optional arguments:
    -h, --help            show this help message and exit
    -o OUTPUT_FILE, --output_file OUTPUT_FILE
                            输出文件的路径
    -n NUMBER, --number NUMBER
                            要处理的数量
    ```

---

## unpacking

!!! note
    unpacking 是指将一个可迭代对象（如列表、元组、字典等）中的元素解包为多个变量。`*` 运算符用于将列表或元组中的元素解包为函数的参数。

```python
def totall(yuan, jiao, fen):
    total = yuan * 100 + jiao * 10 + fen

coins = [1, 1, 1]

print(totall(*coins))
```

- 使用解包操作符 `*` 将 `coins` 列表的元素作为参数传递给  `totall` 函数。如果传递给函数的参数数量不匹配，Python 会抛出一个 `TypeError` 异常，并显示一条错误消息。

```python
package = {"yuan": 1, "jiao": 1, "fen": 1}

print(totall(**package))
```

- 使用解包操作符 `**` 将 `package` 字典中的键值对作为关键字参数传递给 `totall` 函数。

```python
def f(*args, **kwargs):
    print(args)
    print(kwargs)  

# e.g.
f(1, 2, 3, a=4, b=5)
```

- 示例结果：

```python
(1, 2, 3)
{'a': 4, 'b': 5}
```

- `*args`：用于将可变数量的位置参数传递给函数。`args` 是一个元组，包含所有传递给函数的位置参数。

- `**kwargs`：用于将可变数量的关键字参数传递给函数。`kwargs` 是一个字典，包含所有传递给函数的关键字参数。

!!! Info "Attention"
    `*args` 和 `**kwargs` 可以同时使用，但 `*args` 必须在 `**kwargs` 之前，否则会引发语法错误。

---

## map

```python
numbers = [1, 2, 3, 4]
squared = list(map(lambda x: x**2, numbers))
```

- `map()`：接受两个参数：一个函数和一个序列。函数用于处理序列中的每个元素，并返回一个新的序列。

---

## filter

```python
numbers = [1, 2, 3, 4, 5]
even_numbers = list(filter(lambda x: x % 2 == 0, numbers))
```

- `filter()`：接受两个参数：一个函数和一个序列。函数用于测试序列中的每个元素，如果函数返回 True，则该元素会被包含在结果中。

---

## enumerate

```python
for idx, value in enumerate(['a', 'b', 'c']):
    print(f"Index {idx}: {value}")
```

- `enmuerate(iterable, start)` 函数用于遍历序列，并返回每个元素的索引和值。其中， `iterable` 是要遍历的序列，`start` 是索引的起始值，默认为 0。

---

## yield

```python
def countdown(n):
    while n > 0:
        yield n
        n -= 1

for i in countdown(5):
    print(i)

# or
gen = countdown(5)
while True:
    try:
        print(next(gen))
    except StopIteration:
        break
```

!!! note
    If it is return, when the n is too large, it will cause memory error.

    If it is yield, it will not cause memory error.

    它会给一个输出再给一个输出，而不是一次性输出

---

## pyttsx3

!!! Info
    要使用以下函数，需要 `import pyttsx3` 。

!!! note
    `pyttsx3` 是一个用于将文本转换为语音的 Python 库。

```python
engine = pyttsx3.init()
```

- 初始化语音引擎

```python
engine.setProperty('rate', 150)
```

- 设置语速

```python
engine.setProperty('volume', 1)
```

- 设置音量

```python
engine.say("Hello, this is an example of pyttsx3.")
```

- 让引擎发出语音

