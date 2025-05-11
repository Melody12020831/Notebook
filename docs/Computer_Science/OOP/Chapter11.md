---
statistics: True
comments: true
---

# Chapter 11 | templates

## Function overloading

- Same function name with different argument-lists.

```cpp
void print(char * str, int width); // #1
void print(double d, int width); // #2
void print(long l, int width); // #3
void print(int i, int width); // #4
void print(char *str); // #5
print("Pancakes", 15); // #1
print("Syrup"); // #5
print(1999.0, 10); // #2
print(1999, 12); // #4
print(1999L, 15); // #3
```

- c++ 提供的基本的多态性的抽象手段，给一个同名函数，允许同名函数定义多份，每一个同名函数的参数表是不一样的。
- 当上述的 `print` 函数被调用的时候，根据传进去的实参的类型和个数，编译器可以判断调用哪一个版本。

---

## Overload and auto-cast

- 在隐式转换存在时， function overloading 可能会存在一些问题。

```cpp
void foo(int i) {}
void foo(double d) {}

int main(){
    foo(2);
    foo(2.3);
    foo('a');
    foo(3.2f);
    foo(2L);  // Error: call of overloaded ‘foo(long int)’ is ambiguous
}
```

- `char` 到 `int` 存在隐式转换，所以 `'a'` 被转换成 `int` 传给 `foo(int i)` 。
- `L` 是 `long` 类型，可以转换成 `int` 也可以转换成 `double`,所以要么给一个 `foo(long l)` 要么对 `2L` 进行强制的类型转换。

---

## Default arguments

- A default argument is a value given in the declaration that the compiler automatically inserts if you don't provide a value in the function call.

```cpp
int harpo(int n, int m = 4, int j = 5);
beeps = harpo(2); // calls harpo(2,4,5)
beeps = harpo(1,8); // calls harpo(1,8,5)
beeps = harpo(8,7,6);
```

- 在函数声明的某些参数的后面加入一些默认值，这个不是重载，是默认值。例如上述单参数时编译器做了前处理，把后面的两个值传进去，可以认作把默认值填进去了(把源码改了)。
- Default args must be added from right to left.  c++ 中默认值要从右边开始给(大概只是编译器好做)。

```cpp
int chico(int n, int m = 6, int j); //illegal
int groucho(int k = 1, int m = 2, int n = 3);
```

---

## Why templates?

- 对于函数来说，内部逻辑都不一样用 `overloading` 会好一些，但是如果只是参数类型不一样而要每次重写函数就显得笨拙。而对于类来说也是一样的。

- Suppose you need a list of `X` and a list of `Y`

1. The lists would use the same logic
2. The only difference is the type of element

**Possible choices**:

1. Clone the code

- preserves type-safety: 类型检查是安全的
- hard to manage: 重复代码难以管理，容易出现 bug ，因为当更改其中一个版本时另一个大概率也需要更改。

2. Make a common base class

- May not be desirable
- 两个完全不同的类非要说从一个公共的类继承，从设计上来说是不合理的，语义上来说是不直观的。以及纯 O 的方法在运行时是有开销的，虚函数的调用需要额外的开销。

3. Untyped lists

- type unsafe 绕过了类型检查，不太安全。

4. Reuse source code

- generic programming
- use types as parameters in class or function definitions

---

## Templates

1. Function Template

- Example: `sort` function

2. Class Template

- Example: containers -- `stack` , `list` , `queue` , ...
- stack operations are independent of the type of items in the stack
- template member functions

---

### Function templates

- Similar operations on different types of data.
- Swap function for two int arguments:

```cpp
void swap ( int& x, int& y ) {
    int temp = x;
    x = y;
    y = temp;
}
```

- What if we want to swap `floats` , string`s , `Currency` , `Person` ?

```cpp
template < class T >
void swap( T& x, T& y ) {
    T temp = x;
    x = y;
    y = temp;
}
```

- 此时 `T` 是一个占位符，表示任何类型。
- The `template` keyword introduces the template
- The `class T` specifies a parameterized type name
- `class` means any built-in type or UDT(user defined type)
- Inside the template, use T as a type name

??? note "difference between `class` and `typename`"
    在C++模板中，`class T` 和 `typename T` 在声明模板类型参数时**完全等价**，可以互换使用。

    两者的唯一区别是历史习惯：早期C++用 `class` 强调"用户定义类型"，而 `typename` 更明确表示"任意类型"（包括基本类型）。现代 C++ 中推荐用 `typename` 以更通用。

    虽然模板参数声明中二者等价，但 `typename` 在其他场景有**不可替代的作用**，例如在模板体内标记**依赖类型**（Dependent Type）：

    ```cpp
    template<class T>
    void foo() {
        typename T::InnerType x; // 必须用 typename，告诉编译器 InnerType 是类型
    }
    ```

    此处 `T::InnerType` 是依赖模板参数 `T` 的嵌套类型，编译器无法直接确定它是类型还是静态成员，需用 `typename` 明确说明。

---

#### Function templates syntax

Type parameters can represent:

1. types of arguments to the function
2. return type of the function
3. types of local variables within the function

---

#### Template instantiation

Generating a definition from a template class/function and template arguments:

- 先进行**模板参数推断**，编译器根据函数调用或类实例化推断出模板参数的具体类型
- Types are substituted into template 类型替换
- New body of function or class definition is created : syntax errors, type checking 语法检查与类型检查
- Specialization -- a version of a template for a particular argument(s) 编译器会为每个不同的模板参数组合生成一个独立的定义

```cpp
int i = 3; int j = 4;
swap(i, j); // use explicit int swap

float k = 4.5; float m = 3.7;
swap(k, m); // instantiate float swap

std::string s("Hello");
std::string t("World");
swap(s, t); // instantiate std::string swap
```

- A template function is an instantiation of a function template
- 模板定义在这里不会实例化，只有被使用时才会有。不会为所有类型预先生成好。实例化是编译器的行为，只有编译器看到实例化有关的代码时才会进行实例化。
- 而普通函数一定义，函数体一放，编译以后就会有相关代码。所以模板不是真正的函数体，而只是一个板子。

---

#### Template arguments deduction

1. Only exact match on types is used
2. No conversion operations are applied

```cpp
swap(int, int); // ok
swap(double, double); // ok
swap(int, double); // error! 此时不知道 T 究竟是哪个
```

3. Even implicit conversions are ignored

- 模板推导的时候是不允许隐私转换的。必须实际参数和模板完全匹配。

4. Template functions and regular functions coexist

- 尖括号里面是要用到的实例化的版本的类型参数。
- 用尖括号的时候相当于是不需要类型推演，此时就可以执行隐式转换了。

```cpp
#include <iostream>
using namespace std;

template <class T>
void print(T a, T b) {
    cout << a << ", " << b << endl;
}

void print(float a, float b) {
    cout << "print(float):" << a << "," << b << endl;
}


int main() {
    print(2.3f, 5.3f); // print(float):2.3,5.3
    print(2.3, 5.3); // 2.3, 5.3
    print(2, 2.3); // Error
    print<int>(2, 2.3); // print(int):2,2
    print(2, 3.4);      // print(float):2,3.4
}
```

- 实参列表给出来之后，会先找普通函数有没有匹配的。有的话先用普通函数的，没有的话才会去调用模板函数。

---

##### Overloading rules

- First, check for exact regular-function match
- Then, check for exact function-template match
- Last, implicit conversions for regular functions

```cpp
void f(float i, float k) { /*...*/ };
template <class T> void f(T t, T u) { /*...*/ };
f(1.0f, 2.0f);
f(1.0, 2.0);
f(1, 2);
f(1, 2.0);
```

---

#### Function instantiation

- The compiler deduces the template type from the actual arguments passed into the function.
- Types can also be explicitly provided:

e.g. when `T` is not used in the args, but in the function body.

```cpp
template <class T>
void foo() { /* ... */ }
foo<int>(); // type T is int
foo<float>(); // type T is float
```

---

### Class templates

Classes parameterized by types

- Abstract operations from the types being operated upon
- Define potentially infinite set of classes
- Another step towards reuse
- Typical use: container classes

    - `stack<int>`
    - `list<Person*>`
    - `queue<Job>`

---

#### Example: Vector

```cpp
template <class T>
class Vector {
public:
    Vector(int);
    ~Vector();
    Vector(const Vector&);
    Vector& operator=(const Vector&);
    T& operator[](int);
private:
    T* m_elements;
    int m_size;
};
```

---

#### Usage

```cpp
Vector<int> v1(100);
Vector<Complex> v2(256);
v1[20] = 10;
v2[20] = Complex(cos(pi/4), sin(pi/4));
```

- 实例化了之后才有真正的类的定义。

---

#### Vector members

```cpp
template <class T>
Vector<T>::Vector(int size): m_size(size) {
    m_elements = new T[m_size];
}

template <class T>
T& Vector<T>::operator[](int index) {
    if(index < m_size && index >= 0) {
    return m_elements[index];
    } else {
    /*...*/
    }
}
```

---

### A simple sort function

```cpp
// bubble sort – don't use it!
template <class T>
void sort(Vector<T>& arr) {
    const size_t last = arr.size() - 1;
    for (int i = 0; i < last; ++i)
    for (int j = last; j > i; --j) {
        if (arr[j] < arr[j-1]) {
        // which swap?
        swap(arr[j], arr[j-1]);  // 在实例化时才会知道
    }
    }
}
```

- `T` 要有良好的 `copy constructor`，同时 `assignment` 那么也需要一个良好的 `constructor。`

---

#### Sorting the Vector

```cpp
Vector<int> vi(4);
vi[0] = 4; vi[1] = 3; vi[2] = 7; vi[3] = 1;
sort(vi); // sort(Vector<int>&)

Vector<string> vs(5);
vs[0] = "Fred";
vs[1] = "Wilma";
vs[2] = "Barney";
vs[3] = "Dino";
vs[4] = "Prince";
sort(vs); // sort(Vector<string>&);
```

- NOTE: sort use `operator<` for comparison

---

### Templates' properties

1. Templates can use multiple type parameters

模板可以接受多个独立的类型参数，每个参数在模板定义中均可独立使用。

```cpp
template < class Key, class Value >
class HashTable {
    const Value& lookup (const Key&) const;
    void insert (const Key&, const Value&);
    /* ... */
}
```

- 类型参数可以不止一个，可以有很多个。

2. Templates can be nested – they're just new types!

模板实例化后本身就是一个类型，因此可以作为其他模板的参数，形成嵌套结构。

```cpp
Vector< Vector<double*> >
```

!!! info "语法注意"
    在 C++11 前，连续的两个 `>` 需写成 `> >`（避免被解析为右移运算符）， C++11 后已修复此问题。

3. Type arguments can be complicated

模板的类型参数可以是任意合法的 C++ 类型，包括函数指针、嵌套类型等复杂类型。

```cpp
Vector< int (*) (Vector<double>&, int) >
```

- `int (*)(Vector<double>&, int)` 表示一个函数指针，该函数的返回值是 `int`，参数列表里有 `Vector<double>&` (接受一个 `double` 类型的 `Vector` 的引用)和 `int`。

- 模板这一套是图灵完备的，很多都可以做。这意味着通过模板元编程（Template Metaprogramming, TMP），你可以在编译期间完成任意可计算的操作（即任何图灵机能解决的问题）。

??? note "图灵完备"
    一个系统或编程语言被称为图灵完备，如果它能够模拟**图灵机**的计算能力。具体来说，需要支持以下能力：

    - **条件分支**（如 `if`/`else`）
    - **循环或递归**（用于重复操作）
    - **数据存储与操作**（如变量）

    C++模板通过**递归实例化**和**模板特化**实现了这些能力，因此是图灵完备的。

    那么模板如何实现图灵完备？

    **(1) 条件分支：通过模板特化**

    模板特化允许根据不同的类型或值选择不同的实现，类似 `if`/`else` 逻辑。

    ```cpp
    // 通用模板（类似 "else" 分支）
    template<int N>
    struct Factorial {
        static const int value = N * Factorial<N - 1>::value;
    };

    // 特化模板（类似 "if" 分支，终止递归）
    template<>
    struct Factorial<0> {
        static const int value = 1;
    };

    // 编译时计算 5! 
    int result = Factorial<5>::value; // 等价于 120
    ```

    此例中，模板通过递归实例化和特化实现了阶乘计算。

    **(2) 循环：通过递归模板实例化**

    C++ 模板不支持传统循环（如 `for`/`while`），但通过递归实例化可以模拟循环。

    ```cpp
    // 计算 1+2+...+N 的模板元编程
    template<int N>
    struct Sum {
        static const int value = N + Sum<N - 1>::value;
    };

    template<>
    struct Sum<0> {
        static const int value = 0;
    };

    int sum = Sum<5>::value; // 编译时计算 15
    ```

    **(3) 数据存储与操作：通过类型和值包装**

    模板参数可以是类型或值（如 `int`），通过嵌套模板可以构建复杂的数据结构。

    ```cpp
    // 编译时链表结构
    template<typename T, typename Next>
    struct Node {
        using Value = T;
        using NextNode = Next;
    };

    struct End {}; // 链表终止标记

    using MyList = Node<int, Node<float, Node<double, End>>>;
    ```

    **为什么说模板是图灵完备的？**

    - 理论上，只要编译器允许无限递归实例化，模板可以完成任何计算。但实际中，编译器会限制递归深度（如MSVC默认500层，GCC默认900层）。
    - 模板的递归、条件分支和值计算能力，等价于图灵机的计算模型。

    **模板元编程的优缺点**

    | **优点**                     | **缺点**                          |
    |:----------------------------:|:---------------------------------:|
    | 零运行时开销（编译期完成计算） | 代码可读性差（模板代码复杂难懂）   |
    | 类型安全（编译期检查错误）     | 编译时间显著增加（递归实例化开销大）|
    | 实现高度泛化的代码（如STL）   | 调试困难（错误信息冗长晦涩）       |

---

#### Expression parameters

Non-type parameters: may have default arguments

```cpp
template <class T, int bounds = 100>
class FixedVector {
public:
    FixedVector();
    T& operator[](int);
private:
    T elements[bounds]; // fixed-size array!
}
```

- 进来是常数，所以可以作为数组的长度。

```cpp
#include <iostream>
using namespace std;

template <class T, int N>
class Array {
public:
    int size() const {return N;}
    T& operator[](int i) {return m_arr[i];}
private:
    T m_arr[N];
};

int main() {
    Array<int, 3> a;
    a[0] = 2, a[1] = 3, a[2] = 1;
    cout << a.size() << endl;  // 3
    
    Array<int, 3> b{}; // 有花括号已经初始化过了，编译器默认填 0
    cout << b[0] << ", "  << b[1] << ", " << b[2] << endl;  // 0, 0, 0

    b = a;
    cout << b[0] << ", "  << b[1] << ", " << b[2] << endl;  // 2, 3, 1
}
```

- 这样比原生数组方便多了，但是如果是 `Array<int, 3>` 和 `Array<int, 4>` 的话，那么就不能用 `=` 了，因为它们不是同一个类型。而如果用表达式，例如 `Array<int, 9/3>`，那么就可以用 `=` 了，因为它们是同一个类型。但是这个表达式必须是常量表达式，必须要让编译器能够算出来。
- `b = a;` 可以执行是因为编译器生成了默认的拷贝赋值运算符（copy assignment operator），并且该运算符执行的是成员逐拷贝（member-wise copy）。默认的拷贝赋值运算符会逐个拷贝每个非静态成员变量（包括数组），使用成员自身的拷贝赋值运算符。

---

#### Non-type parameters

1. Usage

```cpp
FixedVector<int, 50> v1;
FixedVector<int, 10*5> v2;
FixedVector<int> v3; // => FixedVector<int, 100>
```

2. Summary

- Embedding sizes is not necessarily good
- Can make code run faster
- More complicated code : size argument appears everywhere
- May lead to (even more) code bloat

---

### Member templates

- Template declarations can appear inside a member specification of any class

e.g., a template constructor in `std::complex` :

```cpp
template<typename T> class complex
{
public:
    template<class X> complex(const complex<X>&);
    /* ... */
};
```

---

### Templates and inheritance

1. Templates can inherit from non-template classes 模板类继承自非模板类

```cpp
template <class A>
class Derived : public Base { /* ... */ };
```

2. Templates can inherit from class templates 模板类继承自模板类

```cpp
template <class A>
class Derived : public List<A> { /* ... */ };
```

3. Non-template classes can inherit from instantiated template classes 非模板类继承自实例化的模板类

```cpp
class SupervisorGroup : public List<Employee*> { /* ... */ }
```

- 有具体类之后和普通类也就是一样的。

```cpp
#include <iostream>
using namespace std;

template <typename T>
struct complex{
    T real, imag;
    complex(T real, T imag): real(real), imag(imag) {}
    
    template <typename U>
    complex(const complex<U>& other): real(other.real), imag(other.imag) {}
};

template <typename T>
ostream& operator<<(ostream& out, const complex<T>& c) {
    return out << "(" << c.real << ", " << c.imag << ")";
}

int main() {
    complex<double> a(3.14, -1.57);
    cout << a << endl; // (3.14, -1.57)

    complex<double> b = a;
    cout << b << endl; // (3.14, -1.57) 因为 copy constructor 会自动生成

    complex<int> c = a;
    cout << c << endl; // (3, -1)
}
```

---

## CRTP

- 奇异重现模板模式 CRTP(Curiously Recurring Template Pattern)

```cpp
template <class T>
class Base
{
    /* ... */
};
class Derived : public Base<Derived>
{
    /* ... */
};
```

- 把自己作为类型参数扔了进去。 

---

### Example

```cpp
#include <iostream>
#include <cmath>
using namespace std;

bool is_close(double f, double tolerance){
    return std::fabs(f) < tolerance;
}

void print_info(int k, double x, double f){
    cout << "k = " << k << ", x = " << x << ", f(x) = " << f << endl;
}

class Problem{
public:
    virtual double f(double x) const = 0;
    virtual double df(double x) const = 0;
};

double newton_solve(const Problem* p, double x0, double tolerance = 1e-12, int max_iters = 30){
    int k = 0;
    double x = x0;
    double f = p->f(x);
    double df = p->df(x);

    print_info(k, x, f);

    while(!is_close(f, tolerance) && k < max_iters){
        x = x - f / df;
        f = p->f(x);
        df = p->df(x);
        k++;
        print_info(k, x, f);
    }

    return x;
}

class Sqrt2 : public Problem{
public:
    double f(double x) const override{
        return x * x - 2;
    }

    double df(double x) const override{
        return 2 * x;
    }
};

class WhatEver : public Problem{
public:
    double f(double x) const override{
        return std::cos(x) - std::pow(x, 3);
    }

    double df(double x) const override{
        return -std::sin(x) - 3 * std::pow(x, 2);
    }
};

int main(){
    double x0 = 1.0;

    Sqrt2 sqrt_problem;
    WhatEver what_problem;

    newton_solve(&sqrt_problem, x0);
    cout << "---------------------------------------" << endl;
    newton_solve(&what_problem, x0);
}
```

输出:

```bash
k = 0, x = 1, f(x) = -1
k = 1, x = 1.5, f(x) = 0.25
k = 2, x = 1.41667, f(x) = 0.00694444
k = 3, x = 1.41422, f(x) = 6.0073e-06
k = 4, x = 1.41421, f(x) = 4.51061e-12
k = 5, x = 1.41421, f(x) = 4.44089e-16
---------------------------------------
k = 0, x = 1, f(x) = -0.459698
k = 1, x = 0.880333, f(x) = -0.0453512
k = 2, x = 0.865684, f(x) = -0.000632313
k = 3, x = 0.865474, f(x) = -1.2892e-07
k = 4, x = 0.865474, f(x) = -5.21805e-15
```

- 如果基类 `Problem` 定义了 `virtual` 函数且派生类函数签名（参数、返回类型、const 修饰符等）完全一致，省略 `override` 不会影响功能，但会失去编译器的安全检查。

---

- 如果使用模板来实现呢。

```cpp
#include <iostream>
#include <cmath>
using namespace std;

bool is_close(double f, double tolerance){
    return std::fabs(f) < tolerance;
}

void print_info(int k, double x, double f){
    cout << "k = " << k << ", x = " << x << ", f(x) = " << f << endl;
}

template <typename Problem>
double newton_solve(const Problem* p, double x0, double tolerance = 1e-12, int max_iters = 30){
    int k = 0;
    double x = x0;
    double f = p->f(x);
    double df = p->df(x);

    print_info(k, x, f);

    while(!is_close(f, tolerance) && k < max_iters){
        x = x - f / df;
        f = p->f(x);
        df = p->df(x);
        k++;
        print_info(k, x, f);
    }

    return x;
}

class Sqrt2{
public:
    double f(double x) const { 
        return x * x - 2;
    }

    double df(double x) const {
        return 2 * x;
    }
};

class WhatEver{
public:
    double f(double x) const{
        return std::cos(x) - std::pow(x, 3);
    }

    double df(double x) const{
        return -std::sin(x) - 3 * std::pow(x, 2);
    }
};

int main(){
    double x0 = 1.0;

    Sqrt2 sqrt_problem;
    WhatEver what_problem;

    newton_solve(&sqrt_problem, x0);
    cout << "---------------------------------------" << endl;
    newton_solve(&what_problem, x0);
}
```

输出:

```bash
k = 0, x = 1, f(x) = -1
k = 1, x = 1.5, f(x) = 0.25
k = 2, x = 1.41667, f(x) = 0.00694444
k = 3, x = 1.41422, f(x) = 6.0073e-06
k = 4, x = 1.41421, f(x) = 4.51061e-12
k = 5, x = 1.41421, f(x) = 4.44089e-16
---------------------------------------
k = 0, x = 1, f(x) = -0.459698
k = 1, x = 0.880333, f(x) = -0.0453512
k = 2, x = 0.865684, f(x) = -0.000632313
k = 3, x = 0.865474, f(x) = -1.2892e-07
k = 4, x = 0.865474, f(x) = -5.21805e-15
```

- 这个方案不好的地方在于使用时需要用户自己去看文档来知道如何使用，需要定义的东西(例如本例中的 `f` 和 `df`)。

---

```cpp
#include <iostream>
#include <cmath>
using namespace std;

bool is_close(double f, double tolerance){
    return std::fabs(f) < tolerance;
}

void print_info(int k, double x, double f){
    cout << "k = " << k << ", x = " << x << ", f(x) = " << f << endl;
}

template <typename Derived>
class Problem{
public:
    double f(double x) const{
        return static_cast<const Derived*>(this)->f(x);
    }
    double df(double x) const{
        return static_cast<const Derived*>(this)->df(x);
    }
};

template <typename Derived>
double newton_solve(const Problem<Derived>* p, double x0, double tolerance = 1e-12, int max_iters = 30){
    int k = 0;
    double x = x0;
    double f = p->f(x);
    double df = p->df(x);

    print_info(k, x, f);

    while(!is_close(f, tolerance) && k < max_iters){
        x = x - f / df;
        f = p->f(x);
        df = p->df(x);
        k++;
        print_info(k, x, f);
    }

    return x;
}

class Sqrt2 : public Problem<Sqrt2>{
public:
    double f(double x) const {  
        return x * x - 2;
    }

    double df(double x) const {
        return 2 * x;
    }
};

class WhatEver : public Problem<WhatEver>{
public:
    double f(double x) const {
        return std::cos(x) - std::pow(x, 3);
    }

    double df(double x) const {
        return -std::sin(x) - 3 * std::pow(x, 2);
    }
};

int main(){
    double x0 = 1.0;

    Sqrt2 sqrt_problem;
    WhatEver what_problem;

    newton_solve(&sqrt_problem, x0);
    cout << "---------------------------------------" << endl;
    newton_solve(&what_problem, x0);
}
```

输出:

```bash
k = 0, x = 1, f(x) = -1
k = 1, x = 1.5, f(x) = 0.25
k = 2, x = 1.41667, f(x) = 0.00694444
k = 3, x = 1.41422, f(x) = 6.0073e-06
k = 4, x = 1.41421, f(x) = 4.51061e-12
k = 5, x = 1.41421, f(x) = 4.44089e-16
---------------------------------------
k = 0, x = 1, f(x) = -0.459698
k = 1, x = 0.880333, f(x) = -0.0453512
k = 2, x = 0.865684, f(x) = -0.000632313
k = 3, x = 0.865474, f(x) = -1.2892e-07
k = 4, x = 0.865474, f(x) = -5.21805e-15
```

- 进来的是基类的指针，但是调出来的结果是派生类里面的。看起来像多态，但是不是虚函数，没有运行时开销，是模板做出来的。
- 对于 `Sqrt2` 和 `WhatEver` ，它们的基类是不同的，因为基类是带有模板的。因此如果需要放到一个 `vector` 里面还需要再做一个公共的基类和 `virtual function` 。
- `static_cast` 用于基类到派生类的安全向下转型，结合模板参数确保类型正确。
- `CRTP` 通过模板继承实现编译时多态，避免虚函数开销，提升性能。

---

- Simulate virtual function in generic programming

```cpp
template <class T> 
struct Base { 
    void interface() { // normal
        static_cast<T*>(this)->implementation();
    }
    static void static_func() { // static
        T::static_sub_func();
    }
};
struct Derived : public Base<Derived> { 
    void implementation(); 
    static void static_sub_func(); 
};
```

- 用普通函数可以做，用 `static function` 也可以做。

---

## Morality

- Put the definition/declaration for templates in the header file (因为要实例化必须要看到源码，没有源码无法实例化)
- won't allocate storage for the function/class at that point
- compiler/linker have mechanisms for removing multiple definitions

- main.cpp

```cpp
#include "templates.h"

int main(){
    foo(3);
    foo1(4.3);
}
```

- templates.h

```cpp
#include <iostream>

template <class T>
void foo(T a){
    std::cout <<  a << std::endl;
}

void foo1(double a){
    std::cout <<  a << std::endl;
}
```

- templates.cpp

```cpp
#include "templates.h"

void bar(){
    foo(2);
    foo1(3.2);
}
```

- 此时会有编译错误，但是如果没有 `foo1` 就不会报错。
- 因为模板本身不是实际函数，而是生成函数的"蓝图"。编译器在每个使用模板的源文件中实例化具体类型（如 `foo<int>`），并生成代码。模板实例化后的函数会被标记为弱符号（Weak Symbol），链接器会合并重复的实例化代码，避免冲突。
- 这和 `inline` 类似，都是加了 `week_definition` 。
- 但是非模板函数的定义直接生成强符号（Strong Symbol）。每个包含头文件的源文件（如 `main.cpp` 和 `templates.cpp`）都会生成独立的 `foo1` 定义。强符号不允许重复，导致 `multiple definition` 错误。

---

## Writing templates

1. Get a non-template version working first

先让非模板版本正常工作，确保基础逻辑正确，避免在模板化过程中同时处理逻辑错误和泛型复杂性。

2. Establish a good set of test cases

建立完善的测试用例，通过测试覆盖所有关键场景，为模板化后的代码提供验证基准。

3. Measure performance and tune

测量性能并优化，确保非模板版本的性能足够高效，避免模板化后放大性能问题。

4. Review implementation : Which type(s) should be parameterized?

审查实现：确定需要参数化的类型。明确哪些部分需要泛型化，避免过度设计或遗漏关键参数。

5. Convert the non-parameterized version into a template

将非参数化代码转换为模板，通过泛型化扩展代码的适用性，支持多种类型。

6. Test it against the established test cases

用既有测试用例测试模板代码，验证模板化后的代码与原行为一致，确保泛型化未引入错误。

---

## Further reading

<div class="card file-block" markdown="1">
<div class="file-icon"><img src="/Notebook/assets/images/pdf.svg" style="height: 3em;"></div>
<div class="file-body">
<div class="file-title"> Effective C++__Item-41 </div>
<div class="file-meta"> 92 KB / 2025-04-28</div>
</div>
<a class="down-button" target="_blank" href="/Notebook/Computer_Science/OOP/[Further Readings] Effective C++__Item-41.pdf" markdown="1">:fontawesome-solid-download: 下载</a>
</div>

---