---
statistics: True
comments: true
---

# Chapter 10 | Operator Overloading && Streams

- Allow user-defined types to act like built-in types
- Another way to make a function call

---

## Overloadable operators

### Unary and binary operators overloadable

```cpp
+ - * / % ^ & | ~
= < > += -= *= /= %=
^= &= |= << >> >>= <<= ==
!= <= >= ! && || ++ --
, ->* -> () []
new new[]
delete delete[]
```

---

### You cannot overload:

```cpp
. .* :: ?:
sizeof typeid
static_cast dynamic_cast
const_cast reinterpret_cast
```

---

## Operator Overloading

### Restrictions

- Only existing operators can be overloaded
    - You cannot create ** for exponentiation
- Overloaded operators must
    - Preserve number of operands (一元运算符或二元运算符等)
    - Preserve precedence

---

### Overloaded operators

- just a function with an operator name!
    - Use the operator keyword as a prefix
        - `operator*(...)`

---

- A member function with implicit first argument

`String String::operator+(const String& that);`

- A global (free) function with explicit arguments

`String operator+(const String& l,const String& r);`

---

#### Operator as a member function

```cpp
class Integer{
public :
    Integer( int n = 0 ):i(n){}
    Integer operator+(const Integer& n)const{
        return Integer(i + n.i);
    }
private:
    int i;
};
```

!!! note
    对于 member function 要记住一点，是存在隐式的参数 this 的。

---

##### Member functions

```cpp
Integer x(1), y(5), z;
x + y; // x.operator+(y);
```

- Implicit first argument
- Full access to the class definition and all fields
- No type conversion performed on receiver (.operator 前面的 也就是 receiver 是不能做隐式转换的)
- 下述的 `x + 3` 可以的原因是，编译器会自动调用 `Integer( int n = 0 ):i(n){}` 将 `3` 转换为 `Integer` 类型。

```cpp
z = x + y // Good
z = x + 3 // Good
z = 3 + y // Error
```

---

- For binary operators ( +, -, *, etc. ), the member functions require one argument.
- For unary operators ( unary -, !, etc. ), the member functions require no arguments:

```cpp
Integer operator-() const { 
    return Integer(-i);
}
...
z = -x; // z.operator=(x.operator-());
```

---

#### Operator as a global function

```cpp
Integer operator+(const Integer&, const Integer&);
Integer x, y;
x + y // operator+(x, y);
```

- 没有隐式参数
- Explicit first argument
- Does not need special access to classes
- May need to be a friend
- Type conversions performed on both arguments

---

##### Global operators (friend)

```cpp
class Integer {
public:
    friend Integer operator+(const Integer&, const Integer&); 
    ...
private:
    int i;
};
Integer operator+(const Integer& lhs, const Integer& rhs)
{
    return Integer( lhs.i + rhs.i ); 
}
```

- Binary operators require two arguments
- Unary operators require one argument
- Conversion:

```cpp
z = x + y; // operator+(x, y)
z = x + 3; // operator+(x, Integer(3))
z = 3 + y; // operator+(Integer(3), y)
z = 3 + 7; // Integer(10) 这里是先 3 + 7 再转换为 Integer(10)，这是一个很自然的 int 的计算
```

If you cannot access private data members, then the global function must use the public interface, e.g., the accessors.

---

## Argument passing

- Pass it as a **const reference** if it is **read-only** (except built-ins).
- Make **member functions const** if they do not change the class (relational operators, + , - , etc.).

---

## Return values

- The return type depends on the expected semantics of the operator, e.g.,
    - `operator+` needs to return a new object
    - logical operators should return `bool` .

---

## Prototypes

函数签名其实是固定的:

- `+-*/%^&|~`
    - `T operator X(const T& l, const T& r)`
- `! && || < <= == >= >`
    - `bool operator X(const T& l, const T& r)`
- `[]`
    - `E& T::operator [](int index)`
    - 吃进去一个整数，其实是一种容器，所以要返回容器里面的数据的类型，又因为可以赋值所以有引用。

---

## Operators ++ and --

How to distinguish postfix from prefix?

- `i++` or `++i`
- 单看参数表，看似无法区分，实际上的实现是如下的。

---

- Postfix forms take an `int` argument
- compiler will pass `0` for that argument.

```cpp
class Integer { 
public: 
    ... 
    Integer& operator++(); //prefix++ 
    Integer operator++(int); //postfix++ 
    Integer& operator--(); //prefix-- 
    Integer operator--(int); //postfix-- 
    ... 
};
```

- 这里的 `int` 是用来占位的，实际上即如下：

```cpp
Integer x(5);
++x; // calls x.operator++();
x++; // calls x.operator++(0);
--x; // calls x.operator--();
x--; // calls x.operator--(0);
```

---

### Implementing `++` and `--`

```cpp
Integer& Integer::operator++() { 
    this->i += 1; // increment 
    return *this; // fetch 
} 
// the int argument is not used so leave it unnamed
Integer Integer::operator++( int ){ 
    Integer old( *this ); // fetch 
    ++(*this); // increment 
    return old; // return 
}
```

- 形成重载关系的 `operator` 还是要利用它们之间的关系的
- 使用 `++(*this);` 可是使得实现 `++` 可以把实现运算的特殊性局限在 `operator++` 中，从而使得两个函数拥有一致性

---

## Relational operators

```cpp
class Integer { 
public: 
    bool operator==( const Integer& rhs ) const; 
    bool operator!=( const Integer& rhs ) const;
    bool operator<( const Integer& rhs ) const; 
    bool operator>( const Integer& rhs ) const; 
    bool operator<=( const Integer& rhs ) const; 
    bool operator>=( const Integer& rhs ) const; 
}
```

---

1. implement `!=` in terms of `==`

```cpp
bool Integer::operator==( const Integer& rhs ) const { 
    return i == rhs.i; 
} 
bool Integer::operator!=( const Integer& rhs ) const { 
    return !(*this == rhs); 
}
```

2. implement `>`, `>=`, `<=` in terms of `<`

```cpp
bool Integer::operator<( const Integer& rhs ) const { 
    return i < rhs.i; 
}
bool Integer::operator>( const Integer& rhs ) const { 
    return rhs < *this; 
} 
bool Integer::operator<=( const Integer& rhs ) const { 
    return !(rhs < *this); 
} 
bool Integer::operator>=( const Integer& rhs ) const { 
    return !(*this < rhs); 
}
```

---

## Operator `[]`

```cpp
Vector v(100); // create a vector of size 100
v[10] = 45;
```

- Must be a member function
- Single argument
- Implies that the object acts like an array
- should return a reference

```cpp
#ifndef _VECTOR_H
#define _VECTOR_H

class Vector {
public:
    Vector(int size) : m_size(size) {
        m_array = new int[size];
    }
    ~Vector() {
        delete[] m_array;
    }
    int& operator[](int index) {
        return m_array[index];
    }
private:
    int* m_array;
    int m_size;
};

#endif
```

- index 往往会做两个版本，还有一个是 `const int&` 的版本，因为对于 `const` 对象也要能用。

---

## Operator `( )`

- A **functor**, which overloads the function call operator, is an object that acts like a function.

```cpp
struct F {
    void operator()(int x) const {
    std::cout << x << "\n";
    }
}; // F is a functor class

F f; // f is a functor
f(2); // calls f.operator()
```

- `F` 是 functor class，`f` 是一个 functor object
- 标准库中很多都使用了 `functor`

- 先实现一个转换的功能。

```cpp
#include <iostream>
#include <vector>
using namespace std;

int main(){
    vector<int> v = {1, 3, 5, 7, 9};

    for(int& x : v){
        x *= 5;
    }

    for(int& x : v){
        x += 3;
    }

    for(int& x : v){
        x = x*x;
    }

    for(int& x : v){
        cout << x << " ";
    }

    cout << endl;
}
```

输出:

```bash
64 324 784 1444 2304
```

---

- 但是从重载、软件设计的角度来说，重复代码多，这种做法并不好，我们可以进行一些抽象。

```cpp
#include <iostream>
#include <vector>
using namespace std;

void transform(vector<int>& v, int (*f)(int)){
    for(int& x : v){
        x = f(x);
    }
}

int main(){
    vector<int> v = {1, 3, 5, 7, 9};

    transform(v, [](int x){return x*5;});
    transform(v, [](int x){return x+3;});
    transform(v, [](int x){return x*x;});

    for(int& x : v){
        cout << x << " ";
    }

    cout << endl;
}
```

- 只引用一次，可以用匿名函数
- `[]` 内是捕捉的环境变量

---

- 如果我们需要乘的数据可变呢？

```cpp
#include <iostream>
#include <vector>
using namespace std;

void transform(vector<int>& v, int (*f)(int)){
    for(int& x : v){
        x = f(x);
    }
}

int main(){
    vector<int> v = {1, 3, 5, 7, 9};

    int a = 5;
    transform(v, [](int x){return x*5;});  // Right
    // transform(v, [a](int x){return x*a;});  // Error
    transform(v, [](int x){return x+3;});
    transform(v, [](int x){return x*x;});

    for(int& x : v){
        cout << x << " ";
    }

    cout << endl;
}
```

- `lamda function` 从环境上下文捕获了一些东西后就不再是一个普通的函数，当 `lambda` 表达式 捕获任何变量（例如 [a]）时，它会变成一个"有状态"的闭包对象，而函数指针是无状态的。二者类型不兼容，因此无法直接转换。如果 `lambda` 不捕获任何变量（例如 `[](int x){return x+3;}`），它可以隐式转换为函数指针。

!!! note "有状态的闭包"
    **闭包** 是一个函数及其相关的引用环境（即它能访问的外部变量）。在 C++ 中，`lambda` 表达式生成的闭包对象可以捕获外部变量，这种捕获行为会赋予闭包"状态"。具体来说：

    - **无状态闭包**：如果 `lambda` **不捕获任何外部变量**，它仅是一个普通的函数逻辑，没有额外的数据需要存储。例如：

    ```cpp
    auto lambda = [](int x) { return x + 1; };
    ```
    
    此时，闭包对象没有成员变量，可以隐式转换为函数指针。

    - **有状态闭包**：如果 `lambda` **捕获了外部变量**（例如 `[a]`），闭包对象内部会生成成员变量来保存这些捕获的值或引用。例如：

    ```cpp
    int a = 5;
    auto lambda = [a](int x) { return x * a; }; // 闭包对象内部会保存 `a` 的副本
    ```
    
    此时，闭包对象包含状态（即捕获的变量），无法转换为函数指针。

    因为函数指针（如 `int (*)(int)`）本质是一个指向代码段中某个函数的指针，它只包含函数的地址，**没有存储数据的能力**。当 `lambda` 捕获变量时，生成的闭包对象实际上是一个类实例，内部会保存捕获变量的副本或引用。例如：

    ```cpp
    int a = 5;
    auto lambda = [a](int x) { return x * a; };
    ```

    编译器会为这个 lambda 生成类似如下的类：

    ```cpp
    class Closure {
    private:
        int a; // 保存捕获的变量
    public:
        Closure(int a) : a(a) {}
        int operator()(int x) const { return x * a; }
    };
    ```

    闭包对象 `lambda` 是 `Closure` 类的一个实例，必须通过 `operator()` 调用，且内部需要访问成员变量 `a`。

- 因此可以引入 `std::function` 来处理有状态闭包。并且再次进行更高层次的抽象。

```cpp
#include <cmath>
#include <iostream>
#include <vector>
#include <functional>
using namespace std;

void transform(vector<int>& v, function<int(int)> f){
    for(int& x : v){
        x = f(x);
    }
}

class mul_by{
public:
    mul_by(int a) : a(a) {}
    int operator()(int x) const {
        return x * a;
    }
private:
    int a;
};

class add_by{
public:
    add_by(int a) : a(a) {}
    int operator()(int x) const {
        return x + a;
    }
private:
    int a;
};

class nth_pow{
public:
    nth_pow(int a) : a(a) {}
    int operator()(int x) const {
        return pow(x, a);
    }
private:
    int a;
};

class line {
public:
    line(int a, int b) : a(a), b(b) {}
    int operator()(int x) const {
        return a * x + b;
    }
private:
    int a, b;
};

class print{
public:
    print(char sep) : sep(sep) {}
    int operator()(int x) const {
        cout << x << sep;
        return x;
    }
private:
    char sep;
};

int main(){
    vector<int> v = {1, 3, 5, 7, 9};

    transform(v, mul_by(5));
    transform(v, add_by(3));
    transform(v, nth_pow(2));
    transform(v, line(2, 1));
    transform(v, line(-1, 0));
    transform(v, print(' ')); cout << endl;
    transform(v, print(',')); cout << endl;
}
```

---

## User-defined type conversions

Compilers perform implicit conversions using:

- single-argument constructors (构造函数单参数)
- type conversion operators (定义类型转换的算子)

---

### Single argument constructors

```cpp
class PathName { 
    string name; 
public: 
    PathName(const string&); 
    ~ PathName(); 
}; 
... 
string abc("abc"); 
PathName xyz(abc); // OK! 
xyz = abc; // OK abc => PathName
```

- 这里的 `abc` 可以隐式地转换，先构造一个 `PathName` 的临时对象，再赋值给 `xyz`，最后销毁临时对象。

```cpp
class One{
public:
    One() {}
};

class Two{
public:
    explicit Two(const One&) {}
};

void f(Two) {}

int main(){
    One one;
    f(Two(one)); // OK
    f(one); // 如果去掉 explicit，则可以由隐式转换
}
```

- 单参数的 `ctor` 大部分情况下加上 `explicit` 会好一点，使得语义更清晰

---

### Conversion operator

```cpp
class Rational { 
public: 
    operator double() const {
        return numerator / (double)denominator;
    }
private:
    int numerator;
    int denominator;
};
Rational r(1,3);
double d = 1.3 * r; // r => double
```

- 如果要实现就要求 `r` 可以隐式转换成 `double` 类型。类中定义了类型转换运算符（`operator double()`）。
- 这个 `operator` 很特殊，因为它的名字就是要转换成的那个类型的名字，且它的返回值就是 `double` 类型的值。
- The function will be called automatically
- Return type is same as the function name

---

## The general form

- `X::operator T()`

1. Operator name is any type descriptor
2. No explicit arguments (类型转换运算符在定义时不需要显式声明任何参数，因为它是类的成员函数，隐式作用于当前对象（即类的实例本身）。其操作对象是 `this` 指针指向的实例，因此无需手动传递参数。)
3. No return type

- A conversion operator can be used to convert an object of one class into an object of

1. another class
2. a built-in type

---

### C++ type conversions

1. Built-in conversions, e.g.,

- char => short => int => float => double
- T[] => T*

2. User-defined type conversions T => C if

- either `C(T)` is a valid constructor call for C (要么在类 C 中定义了转换成类型 `T` 的构造函数)
- or `operator C()` is defined for T (要么在类 T 中定义了转换成类型 `C` 的转换运算符)

- 如果 `C` 是 built-in type 的，第一条路是不行的，因为 built-in type 没有构造函数，所以只能用第二条路。

如果两种都做了呢？

```cpp
class Apple;

class Orange {
public:
    Orange() {}
    Orange(const Apple&) {} // 构造函数, convert Apple to Orange， 加上 explicit 关键字，就可以了
};

class Apple {
public:
    operator Orange() { return Orange(); }  // 转换运算符, convert Apple to Orange
}

void f(Orange o) {}

int main(){
    Apple a;
    f(a);  // Error: ambiguous conversion
}
```

- 两类操作都有，所以有歧义
- Must be careful! Cause lots of problems if called unexpectedly.
- Use explicit conversions
- e.g., declare a member function

```cpp
class Rational {
    /* ... */
    double to_double() const;
};
```

- 这样做，转换能力还在，也不会隐式转换。

---

## Stream

### Why streams?

- Original C I/O used printf, scanf
- Streams introduced in C++
    - C I/O libraries still work
- Advantages of streams
    - Type safety
    - Extensible: overload inserters and extractors
    - More object-oriented
- Disadvantages
    - More verbose ( `std::format` comes in C++20)
    - Might be slower (Turn off synchronization: `std::ios::sync_with_stdio(false);`)

---

### What is a stream?

- Common logical interface to a device
- One-dimension (流是一维的), unidirectional
- Random access on file, but not on `std::cin/cout` (因为是串行所以不能随意定位)

---

### Stream naming convections

| |Input|Output|Header|
|:---:|:---:|:---:|:---:|
|Generic|`istream`|`ostream`|`<iostream>`|
|File|`ifstream`|`ofstream`|`<fstream>`|
|C string|`istrstream`|`ostrstream`|`<strstream>`|
|C++ string|`istringstream`|`ostringstream`|`<sstream>`|

---

### Stream operations

1. Extractors

- Read a value from the stream
- Overload `operator>>`

2. Inserters

- Insert a value into a stream
- Overload `operator<<`

3. Manipulators

- Change the stream state

---

### Kinds of streams

1. Text streams

- Deal with ASCII text
- Perform some characters translation
- 多进行了一层转义

e.g., newline => actual OS file representation

2. Binary streams

- Binary data
- No translation

---

#### Predefined streams

- `cin` : standard input
- `cout` : standard output
- `cerr`: unbuffered error (debugging) output
- `clog` : buffered error (debugging) output

```cpp
#include <iostream>
int i; float f; char c;
char buffer[80];
// Read the next character
cin >> c;
// Read an integer, skips whitespace
cin >> i;
// Read a float and a string separated by whitespace
cin >> f >> buffer;
```

- Extractors skip leading whitespace, in general

---

#### Defining a stream extractor

- Has to be a 2-argument free function

1. The first argument is an `istream&`，流读取后状态就变了，所以也不是 const
2. The second argument is a reference to a value，因为从流中读取的值需要赋给某个变量，所以不是 const

```cpp
istream& operator>>(istream& is, T& obj) {
    // specific code to read obj 
    return is;
}
```

- Return an istream& for chaining

```cpp
cin >> a >> b >> c; // ((cin >> a) >> b) >> c;
```

- Other input operators e.g.

`int get()`

- Returns the next character in the stream
- Returns EOF if no characters left
- Example: copy input to output

```cpp
int ch;
while ((ch = cin.get()) != EOF)
     cout.put(ch);
```

---

#### Formatting using manipulators

Manipulators modify the state of the stream

- `#include <iomanip>`
- Effects hold (usually)
- Example

```cpp
int n;
cout << "enter number in hexadecimal" << endl;
cin >> hex >> n;
```

- A simple printing program

```cpp
#include <iostream>
#include <iomanip>
int main() {
    cout << setprecision(2) << 1230.243 << endl; // 两位有效数字
    cout << setw(20) << "OK!"; // 定义输出宽度
    return 0;
}
```

输出:

```bash
1.2e+03
               OK!
```

- 所以 manipulator 本身不是变量，是控制输入输出的"开关"
- 不带参数的 manipulator 简单一点，可以如下定义。(带参数的比较复杂，因此不讨论)

```cpp
// skeleton for an output stream manipulator 
ostream& manip(ostream& out) { 
    ... 
    return out; 
}
ostream& tab(ostream& out) { 
    return out << '\t'; 
}
cout << "Hello" << tab << "World!" << endl;
```

```cpp
#include <iostream>
#include <cmath>
#include <vector>
#include <functional>

using namespace std;

class Point{
public:
    Point(int x, int y) : x(x), y(y) {}
    friend ostream& operator<<(ostream& out, const Point& p);
private:
    int x, y;
};

ostream& operator<<(ostream& out, const Point& p){
    return out << "(" << p.x << "," << p.y << ")";
}

class LineSegment{
public:
    LineSegment(const Point& p1, const Point& p2) : start(p1), end(p2) {}
    friend ostream& operator<<(ostream& out, const LineSegment& s);
private:
    Point start, end;
};

ostream& operator<<(ostream& out, const LineSegment& s){
    return out << s.start << " -------- " << s.end;
}

int main(){
    Point a(3, 5);
    Point b(7, 8);
    cout << a << endl;
    cout << b << endl;

    LineSegment s(a, b);
    cout << s << endl;
}
```

输出:

```bash
(3,5)
(7,8)
(3,5) -------- (7,8)
```

---