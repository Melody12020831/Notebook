---
statistics: True
comments: true
---

# Python-100-Days

!!! Abstract
    这是我在学习 "Python-100-Days" 时所做的笔记 ([这里指路GitHub链接🔗](https://github.com/jackfrued/Python-100-Days/blob/master/Day01-20/01.%E5%88%9D%E8%AF%86Python.md)) 

## Day03 变量

### 检查变量类型 

- `type()`

---

### 通过 Python 内置的函数来改变变量的类型

- `ord()` ： 将（一个字符的）字符串转换成对应的整数（字符编码）。

---

## Day04 运算符

### 赋值运算符 `:=`

|符号|类型|作用|使用场景|
|:-:|:-:|:-:|:-:|
|=|赋值语句|将右侧的值赋给左侧的变量|只能在独立的语句中使用|
|:=|表达式|在表达式内部赋值并返回值|条件判断、循环、推导式等表达式内|

|符号|语言|作用|常见误用场景|
|:-:|:-:|:-:|:-:|
|=|C|赋值赋值（返回被赋的值）|在条件中误用 = 代替 ==|
|==|C|比较是否相等|无|
|=|Python|赋值（不返回值，是语句）|不能在表达式中使用|
|:=|Python|表达式内赋值（返回被赋的值）|需注意作用域和可读性|

!!! note "example code to show the difference between = and :="
    ```python
    print((a := 10))  # 10
    print(a)          # 10
    a = 10
    # print(a = 11) # 'a' is an invalid keyword argument for print()
    ```

    ```c
    #include<stdio.h>

    int main(){
        int a = 10;
        printf("%d\n", a = 11);
        printf("%d\n", a);
        return 0;
    }
    ```

---

### 优先级

- 比较运算符的优先级高于赋值运算符

---

### 占位符

```python
"""
将华氏温度转换为摄氏温度
"""
f = float(input('请输入华氏温度: '))
c = (f - 32) / 1.8
print('%.1f华氏度 = %.1f摄氏度' % (f, c))
```

上面的代码中，我们对 `print` 函数输出的内容进行了格式化处理， `print` 输出的字符串中有两个 `%.1f` 占位符，这两个占位符会被 `%` 之后的 `(f, c)` 中的两个 `float` 类型的变量值给替换掉，浮点数小数点后保留1位有效数字。如果字符串中有 `%d` 占位符，那么我们会用 `int` 类型的值替换掉它，如果字符串中有 `%s` 占位符，那么它会被 `str` 类型的值替换掉。

Python 中还可以用下面的办法来格式化输出，我们给出一个带占位符的字符串，字符串前面的 `f` 表示这个字符串是需要格式化处理的，其中的 `{f:.1f}` 和 `{c:.1f}` 可以先看成是 `{f}` 和 `{c}` ，表示输出时会用变量 `f` 和变量 `c` 的值替换掉这两个占位符，后面的 `:.1f` 表示这是一个浮点数，小数点后保留1位有效数字。

```python
"""
将华氏温度转换为摄氏温度
"""
f = float(input('请输入华氏温度: '))
c = (f - 32) / 1.8
print(f'{f:.1f}华氏度 = {c:.1f}摄氏度')
```

其实还有一种格式化输出的方式，是 Python 3.8 中增加的新特性。这种格式化输出的方式会同时输出变量名和变量值。

```python
"""
输入半径计算圆的周长和面积
"""
import math

radius = float(input('请输入圆的半径: '))  # 输入: 5.5
perimeter = 2 * math.pi * radius
area = math.pi * radius ** 2
print(f'{perimeter = :.2f}')  # 输出：perimeter = 34.56
print(f'{area = :.2f}')       # 输出：area = 95.03
```

---

## Day05 分支结构

### match 语句

- 类似于 `switch` 语句。
- 其中 `_` 表示默认情况，类似于 `switch` 语句中的 `default` 。

```python
status_code = int(input('响应状态码: '))
match status_code:
    case 400: description = 'Bad Request'
    case 401: description = 'Unauthorized'
    case 403: description = 'Forbidden'
    case 404: description = 'Not Found'
    case 405: description = 'Method Not Allowed'
    case 418: description = 'I am a teapot'
    case 429: description = 'Too many requests'
    case _: description = 'Unknown Status Code'
print('状态码描述:', description)
```

- 还有合并版本

```python
status_code = int(input('响应状态码: '))
match status_code:
    case 400 | 405: description = 'Invalid Request'
    case 401 | 403 | 404: description = 'Not Allowed'
    case 418: description = 'I am a teapot'
    case 429: description = 'Too many requests'
    case _: description = 'Unknown Status Code'
print('状态码描述:', description)
```

---

## Day06 循环结构

### range

- 按照 Python 的编程惯例，我们通常把循环变量命名为 `_` ，表示这个变量在循环中不会被用到。

```python
import time

for _ in range(10):
    print('人生苦短，我学 Python')
    time.sleep(1)
```

---

同样的，`range()` 函数也可以接受两个参数，第一个参数是起始值，第二个参数是终止值，前闭后开区间，即包含起始值，不包含终止值。

```python
# range(start, stop, step)
range(0, 10, 2)  # [0, 2, 4, 6, 8]
range(10, 0, -2)  # [10, 8, 6, 4, 2]
```

---

## Day08 列表

需要说明的是，`[]` 的元素位置可以是 0 到 N - 1 的整数，也可以是 -1 到 -N 的整数，分别称为正向索引和反向索引，其中 N 代表列表元素的个数。对于正向索引，`[0]` 可以访问列表中的第一个元素，`[N - 1]` 可以访问最后一个元素；对于反向索引，`[-1]` 可以访问列表中的最后一个元素，`[-N]` 可以访问第一个元素。

---

### 切片

- 如果希望一次性访问列表中的多个元素，我们可以使用切片运算。
- `[start:end:strride]` 是前闭后开的，也即 `[start, end)` 。
- 如果 `start` 值等于 0，那么在使用切片运算符时可以将其省略；如果 `end` 值等于 N，N 代表列表元素的个数，那么在使用切片运算符时可以将其省略；如果 `stride` 值等于 1，那么在使用切片运算符时也可以将其省略。
- 事实上，我们还可以通过切片操作修改列表中的元素。并且切片替换的元素个数可以与原切片的元素个数不同。

---

### 元素的遍历

- 在循环结构中通过索引运算，遍历列表元素。

```python
languages = ['Python', 'Java', 'C++', 'Kotlin']
for index in range(len(languages)):
    print(languages[index])
```

- 直接对列表做循环，循环变量就是列表元素的代表。

```python
languages = ['Python', 'Java', 'C++', 'Kotlin']
for language in languages:
    print(language)
```

---

### 更改列表元素

#### 添加

- `append()` 方法可以在列表末尾添加一个元素。
- `insert(index, element)` 方法可以在列表的指定位置插入一个元素。

```python
languages = ['Python', 'Java', 'C++']
languages.append('JavaScript')
print(languages)  # ['Python', 'Java', 'C++', 'JavaScript']
languages.insert(1, 'SQL')
print(languages)  # ['Python', 'SQL', 'Java', 'C++', 'JavaScript']
```

---

#### 删除

- `remove(element)` 方法可以删除列表中第一个匹配的元素。如果要删除的元素并不在列表中，会引发 `ValueError` 错误导致程序崩溃，所以要先做判断。当要删除的元素在列表中存在多个时，只会删除第一个匹配的元素。
- `pop(index)` 方法可以删除列表中指定位置的元素，并返回该元素。默认删除列表中的最后一个元素。如果索引的值超出了范围，会引发 `IndexError` 异常，导致程序崩溃。
- `clear()` 方法可以清空列表中的所有元素。
- `del` 语句可以删除列表中的元素，语法与 `pop()` 方法类似。

```python
languages = ['Python', 'SQL', 'Java', 'C++', 'JavaScript']
if 'Java' in languages:
    languages.remove('Java')
if 'Swift' in languages:
    languages.remove('Swift')
print(languages)  # ['Python', 'SQL', C++', 'JavaScript']
languages.pop() # now languages = ['Python', 'SQL', C++']
temp = languages.pop(1)
print(temp)       # SQL
languages.append(temp)
print(languages)  # ['Python', C++', 'SQL']
languages.clear()
print(languages)  # []
items = ['Python', 'Java', 'C++']
del items[1]
print(items)  # ['Python', 'C++']
```

`del` 对应的底层字节码指令是` DELETE_SUBSCR `，而 `pop` 对应的底层字节码指令是 `CALL_METHOD` 和 `POP_TOP` ，前者在性能上更优。

---

### 元素位置和频次

列表的 `index` 方法可以查找某个元素在列表中的索引位置，如果找不到指定的元素，`index` 方法会引发 `ValueError` 错误；列表的 `count` 方法可以统计一个元素在列表中出现的次数。

```python
items = ['Python', 'Java', 'Java', 'C++', 'Kotlin', 'Python']
print(items.index('Python'))     # 0
# 从索引位置1开始查找'Python'
print(items.index('Python', 1))  # 5
print(items.count('Python'))     # 2
# 从索引位置3开始查找'Java'
print(items.index('Java', 3))    # ValueError: 'Java' is not in list
```

---

### 元素排序和反转

列表的 `sort` 操作可以实现列表元素的排序，而 `reverse` 操作可以实现元素的反转。

```python
items = ['Python', 'Java', 'C++', 'Kotlin', 'Swift']
items.sort()
print(items)  # ['C++', 'Java', 'Kotlin', 'Python', 'Swift']
items.reverse()
print(items)  # ['Swift', 'Python', 'Kotlin', 'Java', 'C++']
```

---

### 列表生成式

使用列表生成式创建列表不仅代码简单优雅，而且性能上也优于使用 `for-in` 循环和 `append` 方法向空列表中追加元素的方式。为什么说生成式有更好的性能呢，那是因为 Python 解释器的字节码指令中有专门针对生成式的指令（`LIST_APPEND`指令）；而 `for` 循环是通过方法调用（`LOAD_METHOD` 和 `CALL_METHOD` 指令）的方式为列表添加元素，方法调用本身就是一个相对比较耗时的操作。

```python
# 创建一个取值范围在1到99且能被3或者5整除的数字构成的列表。
items = [i for i in range(1, 100) if i % 3 == 0 or i % 5 == 0]
print(items)
```

---

## Day10 元组

在 Python 语言中，元组也是多个元素按照一定顺序构成的序列。元组和列表的不同之处在于，元组是不可变类型，这就意味着元组类型的变量一旦定义，其中的元素不能再添加或删除，而且元素的值也不能修改。如果试图修改元组中的元素，将引发 TypeError 错误，导致程序崩溃。

但是元组可以拼接，因为此时实际上并不是在修改原始元组，而是创建了一个新的元组对象。

```python
tup1 = (1, 2)
tup2 = (3, 4)
combined = tup1 + tup2  # 新元组 (1, 2, 3, 4)
```

`()` 表示空元组，但是如果元组中只有一个元素，需要加上一个逗号，否则 `()` 就不是代表元组的字面量语法，而是改变运算优先级的圆括号，所以 `('hello', )` 和 `(100, )` 才是一元组，而 `('hello')` 和 `(100)` 只是字符串和整数。

---

### 打包和解包

当我们把多个用逗号分隔的值赋给一个变量时，多个值会打包成一个元组类型；当我们把一个元组赋值给多个变量时，元组会解包成多个值然后分别赋给对应的变量。

```python
# 打包
a = (1, 2, 3)
# 解包
x, y, z = a
```

- 在解包时，如果解包出来的元素个数和变量个数不对应，会引发 `ValueError` 异常，错误信息为：`too many values to unpack` 或 `not enough values to unpack` 。
- 有一种解决变量个数少于元素的个数方法，就是使用星号表达式。通过星号表达式，我们可以让一个变量接收多个值。
- 需要注意两点：
    - 用星号表达式修饰的变量会变成一个列表，列表中有 0 个或多个元素。
    - 在解包语法中，星号表达式只能出现一次。
- 需要说明一点，解包语法对所有的序列都成立，这就意味着我们之前讲的列表、`range`函数构造的范围序列甚至字符串都可以使用解包语法。

```python
a = 1, 10, 100, 1000
i, j, *k = a
print(i, j, k)        # 1 10 [100, 1000]
```

---

### 交换变量的值

在 Python 中，交换两个变量 `a` 和 `b` 的值只需要使用如下所示的代码。三个也是同理的。

```python
a, b = b, a
a, b, c = b, c, a
```

- 需要说明的是，上面的操作并没有用到打包和解包语法，`Python` 的字节码指令中有 `ROT_TWO` 和 `ROT_THREE` 这样的指令可以直接实现这个操作，效率是非常高的。但是如果有多于三个变量的值要依次互换，这个时候是没有直接可用的字节码指令的，需要通过打包解包的方式来完成变量之间值的交换。

---

### 元组和列表的比较

- 元组是不可变类型，不可变类型更适合**多线程环境**，因为它降低了并发访问变量的同步化开销。
- 元组是不可变类型，通常不可变类型在**创建时间**上优于对应的可变类型。

- 当然，Python 中的元组和列表类型是可以相互转换的。

```python
infos = ('hello', 100, True, '四川成都')
print(list(infos))  # ['hello', 100, True, '四川成都']

frts = ['apple', 'banana', 'orange']
# 将列表转换成元组
print(tuple(frts))  # ('apple', 'banana', 'orange')
```

---

## Day11 字符串

- Python 中有一种以 `r` 或 `R` 开头的字符串，这种字符串被称为原始字符串，意思是字符串中的每个字符都是它本来的含义，没有所谓的转义字符。

```python
s1 = '\it \is \time \to \read \now'  # ead \is         ime     o 
                                     # ow
s2 = r'\it \is \time \to \read \now' # \it \is \time \to \read \now
print(s1)
print(s2)
```

- Python 中还允许在\后面还可以跟一个八进制或者十六进制数来表示字符，例如 `\141` 表示小写字母 `a`，`\x61` 也表示小写字母 `a`。

---

### 字符串方法

#### 大小写方法

```python
s1 = 'hello, world!'
# 字符串首字母大写
print(s1.capitalize())  # Hello, world!
# 字符串每个单词首字母大写
print(s1.title())       # Hello, World!
# 字符串变大写
print(s1.upper())       # HELLO, WORLD!
s2 = 'GOODBYE'
# 字符串变小写
print(s2.lower())       # goodbye
# 检查s1和s2的值
print(s1)               # hello, world
print(s2)               # GOODBYE
```

!!! note
    由于字符串是不可变类型，使用字符串的方法对字符串进行操作会产生新的字符串，但是原来变量的值并没有发生变化。所以上面的代码中，当我们最后检查 `s1` 和 `s2` 两个变量的值时， `s1` 和 `s2` 的值并没有发生变化。

---

#### 查找操作

```python
s = 'hello, world!'
print(s.find('or'))      # 8
print(s.find('or', 9))   # -1
print(s.find('of'))      # -1
print(s.index('or'))     # 8
print(s.index('or', 9))  # ValueError: substring not found
```

- `find` 方法找不到指定的字符串会返回 -1， `index` 方法找不到指定的字符串会引发 `ValueError` 错误。
- `find` 和 `index` 方法还有逆向查找（从后向前查找）的版本，分别是 `rfind` 和 `rindex` 。

```python
s = 'hello world!'
print(s.find('o'))       # 4
print(s.rfind('o'))      # 7
print(s.rindex('o'))     # 7
# print(s.rindex('o', 8))  # ValueError: substring not found
```

---

#### 性质判断

```python
s1 = 'hello, world!'
print(s1.startswith('He'))   # False
print(s1.startswith('hel'))  # True
print(s1.endswith('!'))      # True
s2 = 'abc123456'
print(s2.isdigit())  # False
print(s2.isalpha())  # False
print(s2.isalnum())  # True
```

- `isdigit`用来判断字符串是不是完全由数字构成的
- `isalpha`用来判断字符串是不是完全由字母构成的，这里的字母指的是 Unicode 字符但不包含 Emoji 字符
- `isalnum` 用来判断字符串是不是由字母和数字构成的。

---

#### 格式化

```python
s = 'hello, world'
print(s.center(20, '*'))  # ****hello, world****
print(s.rjust(20))        #         hello, world
print(s.ljust(20, '~'))   # hello, world~~~~~~~~
print('33'.zfill(5))      # 00033
print('-33'.zfill(5))     # -0033
```

- `center` 方法把字符串放于指定长度的字符串中间，两边用指定的字符填充
- `rjust` 方法把字符串放于指定长度的字符串右边，左边用指定的字符填充
- `ljust` 方法把字符串放于指定长度的字符串左边，右边用指定的字符填充
- `zfill` 方法把字符串放于指定长度的字符串左边，右边用0填充

1. 用 `print` 函数输出字符串时，还可以用下面的方式对字符串进行格式化。

```python
a = 321
b = 123
print('%d * %d = %d' % (a, b, a * b)) # 321 * 123 = 39483
```

2. 当然，我们也可以用字符串的 `format` 方法来完成字符串的格式

```python
a = 321
b = 123
print('{} * {} = {}'.format(a, b, a * b)) # 321 * 123 = 39483
print('{1} * {0} = {2}'.format(a, b, a * b)) # 123 * 321 = 39483
print('{name} loves {girl}'.format(name='Tom', girl='Rose')) # Tom loves Rose
```

3. `f-string` 格式化字符串

- 在这种以 `f` 打头的字符串中，`{变量名}` 是一个占位符，会被变量对应的值将其替换掉

```python
a = 321
b = 123
print(f'{a} * {b} = {a * b}') # 321 * 123 = 39483
```

---

#### 修剪操作

字符串的 `strip` 方法可以帮我们获得将原字符串修剪掉左右两端指定字符之后的字符串，默认是修剪空格字符。这个方法非常有实用价值，可以用来将用户输入时不小心键入的头尾空格等去掉， `strip` 方法还有 `lstrip` 和 `rstrip` 两个版本。

```python
s1 = '   jackfrued@126.com  '
print(s1.strip())      # jackfrued@126.com
s2 = '~你好，世界~'
print(s2.lstrip('~'))  # 你好，世界~
print(s2.rstrip('~'))  # ~你好，世界
```

---

#### 替换操作

`replace` 方法的第一个参数是被替换的内容，第二个参数是替换后的内容，还可以通过第三个参数指定替换的次数。

```python
s = 'hello, good world'
print(s.replace('o', '@'))     # hell@, g@@d w@rld
print(s.replace('o', '@', 1))  # hell@, good world
```

---

#### 拆分与合并

可以使用字符串的 `split` 方法将一个字符串拆分为多个字符串（放在一个列表中），也可以使用字符串的 `join` 方法将列表中的多个字符串连接成一个字符串。`split` 方法默认使用空格进行拆分。

```python
s = 'I love you'
words = s.split()
print(words)            # ['I', 'love', 'you']
print('~'.join(words))  # I~love~you
s = 'I#love#you#so#much'
words = s.split('#')
print(words)  # ['I', 'love', 'you', 'so', 'much']
words = s.split('#', 2)
print(words)  # ['I', 'love', 'you#so#much']
```

---

## Day13 字典

### 创建字典

```python
dict1 = {'name': 'jackfrued', 'age': 20, 'gender': 'male'} # 直接使用大括号
dict2 = dict(name='jackfrued', age=20, gender='male') # 使用 dict 函数
dict3 = dict(zip('ABCDE', '12345')) # 使用 zip 函数 {'A': '1', 'B': '2', 'C': '3', 'D': '4', 'E': '5'}
dict4 = dict(zip('ABCDE', range(1, 10))) # {'A': 1, 'B': 2, 'C': 3, 'D': 4, 'E': 5}
dict5 = {x: x ** 3 for x in range(1, 6)} # 用字典生成式语法创建字典 {'1': 1, '2': 8, '3': 27, '4': 64, '5': 125}
```

---

## Day16 函数进阶

### `Lambda` 函数

- `lambda` 函数只能有一行代码，代码中的表达式产生的运算结果就是这个匿名函数的返回值。

```python
import functools
import operator

# 用一行代码实现计算阶乘的函数
fac = lambda n: functools.reduce(operator.mul, range(2, n + 1), 1)

# 用一行代码实现判断素数的函数
is_prime = lambda x: all(map(lambda f: x % f, range(2, int(x ** 0.5) + 1)))

# 调用Lambda函数
print(fac(6))        # 720
print(is_prime(37))  # True
```

- `reduce` 函数是 `Python` 标准库 `functools` 模块中的函数，它可以实现对一组数据的归约操作，第一个参数是代表运算的函数，第二个参数是运算的数据，第三个参数是运算的初始值。
- 判断素数的 `lambda` 函数通过 `range` 函数构造了从 `2` 到 $\sqrt{x}$ 的范围，检查这个范围有没有 `x` 的因子。`all` 函数也是 `Python` 内置函数，如果传入的序列中所有的布尔值都是 `True`，`all` 函数返回 `True`，否则 `all` 函数返回 `False`。

---

### 偏函数

- 偏函数是指固定函数的某些参数，生成一个新的函数，这样就无需在每次调用函数时都传递相同的参数。

```python
import functools

int2 = functools.partial(int, base=2)
int8 = functools.partial(int, base=8)
int16 = functools.partial(int, base=16)

print(int('1001'))    # 1001

print(int2('1001'))   # 9
print(int8('1001'))   # 513
print(int16('1001'))  # 4097
```

---

### 装饰器

在 `Python` 中，使用装饰器很有更为便捷的语法糖（编程语言中添加的某种语法，这种语法对语言的功能没有影响，但是使用更加方法，代码的可读性也更强，我们将其称之为"语法糖"或"糖衣语法"），可以用 `@装饰器函数` 将装饰器函数直接放在被装饰的函数上，效果跟上面的代码相同。

```python
import random
import time

from functools import wraps


def record_time(func):

    @wraps(func)
    def wrapper(*args, **kwargs):
        start = time.time()
        result = func(*args, **kwargs)
        end = time.time()
        print(f'{func.__name__}执行时间: {end - start:.2f}秒')
        return result

    return wrapper


@record_time
def download(filename):
    print(f'开始下载{filename}.')
    time.sleep(random.random() * 6)
    print(f'{filename}下载完成.')


@record_time
def upload(filename):
    print(f'开始上传{filename}.')
    time.sleep(random.random() * 8)
    print(f'{filename}上传完成.')


# 调用装饰后的函数会记录执行时间
download('MySQL从删库到跑路.avi')
upload('Python从入门到住院.pdf')
# 取消装饰器的作用不记录执行时间
download.__wrapped__('MySQL必知必会.pdf')
upload.__wrapped__('Python从新手到大师.pdf')
```

- 当你在函数定义前使用 `@record_time` 时，这个装饰器函数 `record_time` 会接收被装饰的原始函数（如 `download` 或 `upload` ）作为参数传入 `func` 参数。`func` 参数用于在装饰器内部记住原始函数，以便后续调用它。
- 在代码中，`@record_time` 语法糖等价于：

```python
download = record_time(download)
upload = record_time(upload)
```

- 使用 `@wraps(func)` 后，装饰后的函数会保留 `__wrapped__` 属性，指向原始函数。通过 `__wrapped__` 可以直接调用未被装饰的函数，也就是避免触发计时逻辑。

---

## Day67 miniconda

!!! info
    其实网站中给的是 Anaconda，但是我安装的是 miniconda，只是因为之前装过。这里记录一下一些使用方法。

- 创建虚拟环境，`-n` 是 `name` 的缩写，`python` 不指定版本就默认最新版

```bash
conda create -n myenv python=3.8
```

- 激活虚拟环境

```bash
activate myenv
```

- 退出当前虚拟环境

```bash
deactivate
```

- 删除虚拟环境

```bash
conda env remove -n myenv
```

- 查看所有虚拟环境

```bash
conda env list
```

---

### JupyterLab 中的快捷键

命令模式下的快捷键：

| 快捷键                                   | 功能说明                                     |
| :--------------------------------------: | :------------------------------------------: |
| `Alt` + `Enter`                          | 运行当前单元格并在下面插入新的单元格         |
| `Shift` + `Enter`                        | 运行当前单元格并选中下方的单元格             |
| `Ctrl` + `Enter`                         | 运行当前单元格                               |
| `j` / `k`、`Shift` + `j` / `Shift` + `k` | 选中下方/上方单元格、连续选中下方/上方单元格 |
| `a` / `b`                                | 在下方/上方插入新的单元格                    |
| `c` / `x`                                | 复制单元格 / 剪切单元格                      |
| `v` / `Shift` + `v`                      | 在下方/上方粘贴单元格                        |
| `dd` / `z`                               | 删除单元格 / 恢复删除的单元格                |
| `Shift` + `l`                            | 显示或隐藏当前/所有单元格行号                |
| `Space` / `Shift` + `Space`              | 向下/向上滚动页面                            |

编辑模式下的快捷键：

| 快捷键                     | 功能说明                               |
| :------------------------: | :------------------------------------: |
| `Shift` + `Tab`            | 获得提示信息                           |
| `Ctrl` + `]`/ `Ctrl` + `[` | 增加/减少缩进                          |
| `Alt` + `Enter`            | 运行当前单元格并在下面插入新的单元格   |
| `Shift` + `Enter`          | 运行当前单元格并选中下方的单元格       |
| `Ctrl` + `Enter`           | 运行当前单元格                         |
| `Ctrl` + `Left` / `Right`  | 光标移到行首/行尾                      |
| `Ctrl` + `Up` / `Down`     | 光标移动代码开头/结尾处                |
| `Up` / `Down`              | 光标上移/下移一行或移到上/下一个单元格 |

---