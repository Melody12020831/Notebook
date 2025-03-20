---
statistics: True
comments: true
---

# Chapter 1 | introduction

## The first CPP program

```cpp
#include<iostream>
using namespace std;
int main() {  
    int age;
    cin >> age;
    cout << "Hello, World! I am " << age << " years old!" << endl;  
    return 0;
}
```

- `iostream` 是定义输入/输出流相关函数和操作的头文件
- 命名空间用于区分具有相同方法名的代码块。在本程序中，使用命名空间 std; 将命名空间设置为标准，以便用户在程序中使用所有标准方法。
- 有些编译器 `void` 可能会报错，要用 `int`
- `cin` 是输入函数，`cout` 是输出函数
- `endl` 是换行符，相当于 `\n`
- 不写 `return 0` 也行

---

## String

### Assignment

```cpp
char cstr1[20];
char cstr2[20] = "jaguar"; 

string str1;
string str2 = "panther"; 

cstr1 = cstr2; // illegal 
str1 = str2; // legal
```

- 数组不能直接 copy 要调用函数 `strcpy(cstr1, cstr2);`
- `string` 可以直接 copy

---

### Concatenation

```cpp
string str1 = "foo";
string str2 = "bar";
string str3 = str1 + str2; 
cout << "str3 = " << str3 << endl; // str3 = foobar


str2 += str1;
cout << "str2 = " << str2 << endl; // str2 = barfoo
```

- 字符串的连接

---

### Constructors(Ctors)

```cpp
string (const char *cp, int len);  // copy from cp to cp+len

string (const string& s2, int pos); // copy from pos

string (const string& s2, int pos, int len); // copy from pos to pos+len
```

!!! note
    `string` 的元素存储是连续的，即对于 `string s` ，对 `[​0​, s.size())` 中的任意 `n` 有 `&*(s.begin() + n) == &*s.begin() + n`。

---

### Substring 

```cpp
substr (int pos, int len);
```

- `substr` 返回一个从 `pos` 开始，长度为 `len` 的子串

---

### Modification

```cpp
str3 = "hello, china!"; // 赋值
string str4("hello, zju"); // 初始化
string str5(str3); // 拷贝构造
string str6(str3, 7, 5);
string str7 = str3.substr(7, 5);
string str8 = str3;
str8.replace(7, 5, "zjg");

cout << "str4 = " << str4 << endl; // str4 = hello, zju
cout << "str5 = " << str5 << endl; // str5 = hello, china!
cout << "str6 = " << str6 << endl; // str6 = china
cout << "str7 = " << str7 << endl; // str7 = china
cout << "str8 = " << str8 << endl; // str8 = hello, zjg!

str8.assign(10, 'A');
cout << "str8 = " << str8 << endl; // str8 = AAAAAAAAAA

string str9 = "hello, hangzhou city!";
cout << "str9 = " << str9 << endl; // str9 = hello, hanghzou city!
string str_to_find = "hangzhou";
cout << "str9.find(str_to_find) = " << str9.find(str_to_find) << endl; // str9.find(str_to_find) = 7
str9.replace(str9.find(str_to_find), str_to_find.length(), "jinhua");
cout << "str9 = " << str9 << endl; // str9 = hello, jinhua city!
```

- 初始化和拷贝构造有本质区别
- 构造函数是一种特殊的成员函数

1. `assign` 函数

- `assign(const string& str)` ：将当前字符串替换为 `str` 的副本。
- `assign( size_type count, CharT ch );` ：将当前字符串替换为 `count` 个字符 `ch` 的副本。

2. `insert` 函数

- `insert( size_type index, size_type count, CharT ch );` ：在字符串的 `index` 位置插入 `count` 个字符 `ch`。
- `insert( size_type index, const CharT* s );` : 在字符串的 `index` 位置插入字符串 `s` 且字符串的长度由首个空字符，通过 `Traits::length(s)` 确定。
- `insert( size_type index, const CharT* s, size_type count );` ：在字符串的 `index` 位置插入插入范围 `[s, s + count)` 中的字符。范围可以包含空字符。
- `insert( size_type index, const string& str );` ：在字符串的 `index` 位置插入字符串 `str` 。
- `iterator insert( iterator pos, CharT ch );` : 在 `pos` 所指向的字符前插入字符 `ch` 。

3. `erase` 函数

- `erase(index,count);` ：删除从 `index` 开始的 `count` 个字符。如果 `count` 超出范围(`std::min(count, size() - index)`)，则删除从 `index` 到字符串末尾的所有字符。如果省略 `count`，则删除从 `index` 到字符串末尾的所有字符。

4. `append` 函数

- `append(count, ch);` ：将 `count` 个字符 `ch` 添加到字符串的末尾。
- `append(const CharT* s, size_type count );` ：将范围 `[s, s + count)` 中的字符添加到字符串的末尾。范围可以包含空字符。
- `append(const CharT* s);` ：等价于 `return append(s, Traits::length(s));`。

5. `replace` 函数

- `replace(pos, count, const string& str );` : 以给定字符替换范围 `[begin() + pos, begin() + std::min(pos + count, size()))`

6. `find` 函数

- `find(string& str, pos) const;` : 寻找首个等于给定字符序列的子串。搜索从 pos 开始，也就是说找到的子串不会从 pos 之前的位置开始。
- `find( const CharT* s, size_type pos, size_type count ) const;` : 寻找首个等于范围 `[s, s + count)` 的子串。此范围可以包含空字符。
- `find( const CharT* s, size_type pos = 0 ) const;` : 寻找首个等于 `s` 所指向的字符串的子串。该字符串的长度由首个空字符，通过 `Traits::length(s)` 确定。

7. `clear` 函数

- `void clear();` : 删除字符串中的所有字符，使其为空字符串。如同通过执行 `erase(begin(), end())`。

??? note "reference"
    - [assign](https://zh.cppreference.com/w/cpp/string/basic_string/assign)

    - [insert](https://zh.cppreference.com/w/cpp/string/basic_string/insert)

    - [erase](https://zh.cppreference.com/w/cpp/string/basic_string/erase)

    - [append](https://zh.cppreference.com/w/cpp/string/basic_string/append)

    - [replace](https://zh.cppreference.com/w/cpp/string/basic_string/replace)

    - [find](https://zh.cppreference.com/w/cpp/string/basic_string/find)

    - [clear](https://zh.cppreference.com/w/cpp/string/basic_string/clear)

---

### files

```cpp
#include <iostream>
#include <fstream>

using namespace std;

int main(){
    string str1 = "foo, bar!";
    ofstream fout("out.txt");  // or ofstream fout("C:\\test.txt");
    fout << str1 << endl;

    ifstream fin("out.txt");
    string str2, str3;
    fin >> str2 >> str3;
    cout << "str2 = " << str2 << endl; // str2 = foo,
    cout << "str3 = " << str3 << endl; // str3 = bar!
}
```

??? note "在 fin 时为什么要有两个呢"
    因为在 `str1` 中有一个空格，在读入时会自动断开。一行全读进来需要用 `getline` 函数。

    `getline` 函数： 定义在头文件 `<string>` 中。

    ```cpp
    std::basic_istream<CharT, Traits>& getline( std::basic_istream<CharT, Traits>& input, std::basic_string<CharT, Traits, Allocator>& str, CharT delim );
    ```

    **Example**:

    ```cpp
    std::string name;
    std::cout << "What is your name? ";
    std::getline(std::cin, name);
    std::cout << "Hello " << name << ", nice to meet you.\n";
    ```

---

### regex

```cpp
#include <iostream>
#include <regex>

using namespace std;

int main(){
    string s = "Hello, Students@zju!";
    regex re("a|e|i|o|u");
    string s1 = regex_replace(s, re, "*");
    cout << "s1 = " << s1 << endl; // s1 = H*ll*, St*d*nts@zj*!
}
```

- 双引号，所以可以是一个串。
- 正则表达式 `a|e|i|o|u`
    - `|` 表示逻辑"或",匹配任意一个小写元音字母`(a、e、i、o、u)`。
    - 注意：正则表达式默认区分大小写，因此大写元音不会被匹配。

---

## Further reading

<div class="card file-block" markdown="1">
<div class="file-icon"><img src="/Notebook/assets/images/pdf.svg" style="height: 3em;"></div>
<div class="file-body">
<div class="file-title"> A_Tour_of_C++__CH08 </div>
<div class="file-meta"> 124 KB / 2025-02-17</div>
</div>
<a class="down-button" target="_blank" href="/Notebook/Computer_Science/OOP/Further_reading/[Further Readings] A_Tour_of_C++__CH08.pdf" markdown="1">:fontawesome-solid-download: 下载</a>
</div>

---