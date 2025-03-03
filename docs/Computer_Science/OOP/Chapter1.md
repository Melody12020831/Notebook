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
string (const string& s2, int pos); // copy from pos

string (const string& s2, int pos, int len); // copy from pos to pos+len
```

---

### Substring | Modification

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

---

### files

```cpp
#include <iostream>
#include <fstream>

using namespace std;

int main(){
    string str1 = "foo, bar!";
    ofstream fout("out.txt");
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
    cout << "s1 = " << s1 << endl; // s1 = H*ll*, St*dn*ts@zju!
}
```

- 双引号，所以可以是一个串。

---


