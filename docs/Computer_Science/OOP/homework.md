---
statistics: True
comments: true
---

!!! abstract
    我把 PTA 上布置的题目整理记录一下，便于期末复习吧。

## 001.5

### Question 1

Adam is implementing a representation class for complex numbers. In Adam's `Complex` class design, the real and imaginary parts of a complex number are explicitly stored as the data members. Please help him to finish the job.

Note that Adam's implementation is not the only choice for representing complex numbers. But with a suitable set of methods (a.k.a., member functions) made public, other developers could easily write stable code by leveraging the abstraction barrier of the `Complex` class.

Compared with the "Complex II" problem, you could notice that the user code is the same, although Eve implements the class differently from Adam. That means once the prototypes of the public methods (i.e., the interface) are stable, you could readily change the underlying implementation details without affecting the users of the class.

```cpp
#include <cmath>
#include <iostream>

// ------------------------------------------------------------------
// Adam's class design starts from here.
//

class Complex
{
private:
  double re, im;
  Complex() {}
public:
  double real() const { return re; }
  double imaginary() const { return im; }
  double magnitude() const { [                              ]; }
  double angle() const { return atan2(im, re); }
public:
  static Complex from_cartesian(double real, double imag)
  {
    Complex c;
    c.re = real;
    c.im = imag;
    return c;
  }
  static Complex from_polar(double magnitude, double angle)
  {
    Complex c;
    c.re = [                                               ];
    c.im = magnitude * sin(angle);
    return c;
  }
};

//
// Adam's class design ends here.
// ------------------------------------------------------------------
// The following code is written by the user of the Complex class.
//

Complex add_complex(const Complex& c1, const Complex& c2)
{
  double real = c1.real() + c2.real();
  double imag = c1.imaginary() + c2.imaginary();
  return Complex::from_cartesian(real, imag);
}

Complex multiply_complex(const Complex& c1, const Complex& c2)
{
  double magnitude = c1.magnitude() * c2.magnitude();
  double angle = c1.angle() + c2.angle();
  return Complex::from_polar(magnitude, angle);
}

void print_complex(const Complex& c)
{
  std::cout << c.real() << " + " << c.imaginary() << "i" << std::endl;
}

int main()
{ 
  Complex c1 = Complex::from_cartesian(3, 4);
  Complex c2 = Complex::from_cartesian(5, 12);

  print_complex(add_complex(c1, c2));
  print_complex(multiply_complex(c1, c2));
}
```

### Answer

```cpp
return std::sqrt(re*re+im*im)
magnitude * cos(angle)
```

---

### Question 2

Eve is implementing a representation class for complex numbers. In Eve's `Complex` class design, the magnitude and angle parts of a complex number (in the polar coordinate system) are explicitly stored as the data members. Please help her to finish the job.

Note that Eve's implementation is not the only choice for representing complex numbers. But with a suitable set of methods (a.k.a., member functions) made public, other developers could easily write stable code by leveraging the abstraction barrier of the `Complex` class.

Compared with the "Complex I" problem, you could notice that the user code is the same, although Adam implements the class differently from Eve. That means once the prototypes of the public methods (i.e., the interface) are stable, you could readily change the underlying implementation details without affecting the users of the class.

```cpp
#include <cmath>
#include <iostream>

// ------------------------------------------------------------------
// Eve's class design starts from here.
//

class Complex
{
private:
  double mag, ang;
  Complex() {}
public:
  double real() const { [                                     ]; }
  double imaginary() const { return mag * sin(ang); }
  double magnitude() const { return mag; }
  double angle() const { return ang; }
public:
  static Complex from_cartesian(double real, double imag)
  {
    Complex c;
    c.mag = [                                                   ];
    c.ang = atan2(imag, real);
    return c;
  }
  static Complex from_polar(double magnitude, double angle)
  {
    Complex c;
    c.mag = magnitude;
    c.ang = angle;
    return c;
  }
};

//
// Eve's class design ends here.
// ------------------------------------------------------------------
// The following code is written by the user of the Complex class.
//

Complex add_complex(const Complex& c1, const Complex& c2)
{
  double real = c1.real() + c2.real();
  double imag = c1.imaginary() + c2.imaginary();
  return Complex::from_cartesian(real, imag);
}

Complex multiply_complex(const Complex& c1, const Complex& c2)
{
  double magnitude = c1.magnitude() * c2.magnitude();
  double angle = c1.angle() + c2.angle();
  return Complex::from_polar(magnitude, angle);
}

void print_complex(const Complex& c)
{
  std::cout << c.real() << " + " << c.imaginary() << "i" << std::endl;
}

int main()
{ 
  Complex c1 = Complex::from_cartesian(3, 4);
  Complex c2 = Complex::from_cartesian(5, 12);

  print_complex(add_complex(c1, c2));
  print_complex(multiply_complex(c1, c2));
}
```

### Answer

```cpp
return mag * cos(ang)
std::sqrt(real * real + imag * imag)
``` 

---

## 002.5

### Question 1

How to create a dynamic array of 20 pointers to integers using the new operator in C++?

A. `int *arr = new int *[20];`

B. `int *arr = new int [20];`

C. `int **arr = new int *[20];`

D. Impossible

### Answer

正确答案是：

**C. `int **arr = new int *[20];`**

解释：

- 要创建一个包含 20 个指向整数的指针的动态数组，你需要分配一个指针数组（`int*`），而不是一个整数数组（`int`）。
- `int **arr` 是一个指向指针的指针，适合用来存储一个指向整数指针数组的地址。
- `new int *[20]` 分配了一个包含 20 个指向整数的指针的数组。

---

### Question 2

Which of the following is TRUE about `new` when compared with `malloc`?

1. `new` is an operator, while `malloc` is a function.
2. `new` calls an appropriate constructor for object allocation, while `malloc` doesn't.
3. `new` returns a pointer with the appropriate type, while `malloc` only returns a `void *` pointer that needs to be typecasted to the appropriate type.

A. 1 and 2

B. 2 and 3

C. 1 and 3

D. All 1, 2 and 3

### Answer

正确答案是：

**D. All 1, 2 and 3**

解释：

1. **`new` 是运算符，而 `malloc` 是函数。**  

   - 在 C++ 中，`new` 是一个关键字，用于动态分配内存，而 `malloc` 是 C 标准库中的一个函数。

2. **`new` 会调用适当的构造函数来分配对象，而 `malloc` 不会。**  

   - 当使用 `new` 分配对象时，它会自动调用对象的构造函数。而 `malloc` 只是分配一块内存，不会调用构造函数。

3. **`new` 返回一个适当类型的指针，而 `malloc` 只返回一个 `void *` 指针，需要强制转换为适当类型。** 
 
   - `new` 直接返回与分配类型匹配的指针（例如 `int*`、`MyClass*` 等），而 `malloc` 返回的是 `void*`，需要手动进行类型转换。

---

## 003.5

### Question

Please show the output of the following program.

```cpp
#include <iostream>

struct X {
    X() {
        std::cout << "X::X()" << std::endl;
    }
    ~X() {
        std::cout << "X::~X()" << std::endl;
    }
};

struct Y {
    Y() {
        std::cout << "Y::Y()" << std::endl;
    }
    ~Y() {
        std::cout << "Y::~Y()" << std::endl;
    }
};

struct Parent {
    Parent() {
        std::cout << "Parent::Parent()" << std::endl;
    }
    ~Parent() {
        std::cout << "Parent::~Parent()" << std::endl;
    }
    X x;
};

struct Child : public Parent {
    Child() {
        std::cout << "Child::Child()" << std::endl;
    }
    ~Child() {
        std::cout << "Child::~Child()" << std::endl;
    }
    Y y;
};

int main() {
    Child c;
}
```

### Answer

```cpp
Line 1: X::X()
Line 2: Parent::Parent()
Line 3: Y::Y()
Line 4: Child::Child()
Line 5: Child::~Child()
Line 6: Y::~Y()
Line 7: Parent::~Parent()
Line 8: X::~X()
```

解释:

**构造顺序**（从内到外，自下而上）

1. 基类的成员构造,`Parent` 是基类，其成员变量 `X x` 会优先构造，调用 `X::X()`。
2. 基类构造函数,基类 `Parent` 的构造函数体 `Parent::Parent()` 执行。
3. 派生类的成员构造, `Child` 是派生类，其成员变量 `Y y` 随后构造，调用 `Y::Y()`。
4. 派生类构造函数, 最后执行派生类 `Child` 的构造函数体 `Child::Child()`。

**析构顺序**（与构造顺序完全相反，从外到内，自上而下）。

**核心原理**：

确保派生类构造时基类已完整初始化，析构时派生类资源先释放，避免依赖基类已销毁的资源。

---

## 004.5

### Question

Please show the output of the following program.

```cpp
#include <iostream>
using namespace std;

class A
{
public:
  A(int i) : mi(i) {}
  A(const A& rhs) : mi(rhs.mi)
  {
    cout << "A::A(&)" << endl;
  }
  A& operator=(const A&rhs)
  {
    mi = rhs.mi;
    cout << "A::operator=()" << endl;
    return *this;
  }
  virtual void f()
  {
    cout << "A::f(), " << mi << endl;
  }
protected:
  int mi;
};

class B : public A
{
public:
  B(int i, int j) : A(i), mj(j) {}
  void f() override
  {
    cout << "B::f(), " << mi << ", " << mj << endl;
  }
private:
  int mj;
};

int main()
{
  A a1(1);
  B b(3,4);

  A& ra = b;
  ra.f();
  ra = a1;
  ra.f();

  A a2 = b;
  a2.f();
}
```

### Answer

```cpp
B::f(), 3, 4
A::operator=()
B::f(), 1, 4
A::A(&)
A::f(), 1
```

程序的输出结果如下：

```
B::f(), 3, 4
A::operator=()
B::f(), 1, 4
A::A(&)
A::f(), 1
```

1. **`ra.f()` 第一次调用：**
   - `ra` 是 `A` 的引用，但指向 `B` 类对象 `b`。
   - 由于 `f()` 是虚函数，触发多态，调用 `B::f()`。
   - 输出：`B::f(), 3, 4`（`mi=3` 继承自 `A`，`mj=4` 是 `B` 的成员）。

2. **`ra = a1` 赋值操作：**
   - `ra` 实际指向 `b` 的 `A` 部分。
   - 调用 `A` 的赋值运算符，将 `a1` 的 `mi=1` 赋值给 `b` 的 `A` 部分。
   - 输出：`A::operator=()`。

3. **`ra.f()` 第二次调用：**
   - `ra` 仍指向 `b`（实际类型是 `B`），虚函数调用仍为 `B::f()`。
   - 此时 `b` 的 `mi` 已被修改为 1，`mj` 保持 4。
   - 输出：`B::f(), 1, 4`。

4. **`A a2 = b` 对象初始化：**
   - 用 `B` 类对象 `b` 初始化 `A` 类对象 `a2`，发生对象切片。
   - 调用 `A` 的拷贝构造函数（只复制 `B` 部分的 `mi=1`）。
   - 输出：`A::A(&)`。

5. **`a2.f()` 调用：**
   - `a2` 是纯 `A` 类对象，调用 `A::f()`。
   - 输出：`A::f(), 1`（`mi=1` 来自拷贝构造）。


**重载赋值运算符**

```cpp
A& operator=(const A& rhs)
```

- **作用**：重载赋值运算符 `=`，用于将一个 `A` 类对象的值赋给另一个 `A` 类对象。
- **参数**：
  - `const A& rhs`：一个常量引用，表示赋值操作右侧（Right-Hand Side）的对象。
- **返回值**：
  - 返回当前对象的引用（`A&`），支持链式赋值（如 `a = b = c`）。

```cpp
{
  mi = rhs.mi;          // 将右侧对象的 mi 赋值给当前对象的 mi
  cout << "A::operator=()" << endl; // 输出提示信息
  return *this;         // 返回当前对象的引用
}
```

---

## 005.5

### Question

```cpp
#include <iostream>
#include <vector>
using namespace std;

class vec3 {
public:
    vec3(int x=0, int y=0, int z=0){
        v[0] = x;
        v[1] = y;
        v[2] = z;
    }
    int operator[]         
    {
        return v[index];
    }
    vec3& operator+=(const vec3& rhs){
    for (int i = 0; i < 3; ++i)
                    ;
                    ;
    }
private:
    int v[3];
};

vec3 operator+(const vec3& v1, const vec3& v2)
{
    return                              ;
};

        operator<<(ostream& out, const vec3& v)
{
    out << '(' << v[0] << ' ' << v[1] << ' ' << v[2] << ')';
              ;
}

int main()
{
    vec3 v1(1,2,3), v2(4,5,6);
    vec3 v = v1 + v2;
    v += v2;
    cout << v << endl;
}
```

### Answer

```cpp
(int index) const
v[i] += rhs.v[i]
return *this
vec3(v1[0]+v2[0], v1[1]+v2[1], v1[2]+v2[2])
ostream&
return out
```

1. `operator[]` 重载: 添加 `int index` 参数和 `const` 修饰符，使其能正确访问元素并支持常量对象。
2. `operator+=` 重载: 在循环中将每个分量与右操作数对应分量相加，并返回 `*this` 以实现链式操作。
3. `operator+` 重载: 通过 `vec3` 构造函数直接创建新对象，其分量为两个操作数对应分量之和。
4. `operator<<` 重载: 添加 `ostream&` 返回类型，并在输出完成后返回流对象以支持连续输出。

---

## 006.5

### Question

The function template `min_elem()` finds the smallest element in the range `[first, last)` and returns the iterator to the smallest element. The way how smallest is understood can be customized.

```cpp
#include <functional>
#include <iostream>
#include <iterator>
#include <string>
#include <list>
#include <vector>

template<class ForwardIt, class Compare>
ForwardIt min_elem(ForwardIt first, ForwardIt last,                 comp)
{
  if (first == last)
    return                      ;

  ForwardIt smallest = first++;
  for (;                   ; ++first) {
    if (comp(*first, *smallest)) {
      smallest = first;
    }
  }
  return                        ;
}

template<class ForwardIt>
ForwardIt min_elem(ForwardIt first, ForwardIt last)
{
  return min_elem(first, last, std::less<                     std::iterator_traits<ForwardIt>::value_type>());
}

struct Student {
  int id;
  std::string name;
  bool                                 (const Student& s2) const {
    return id < s2.id;
  }
};

std::ostream& operator<<(std::ostream& out, const Student& s)
{
  out << s.name << s.id;
  return out;
}

int main()
{
  std::vector<int> v = { 3, 1, 4, 2, 5, 9 };
  std::cout << "min element is: " << *min_elem(std::begin(v), std::end(v)) << std::endl;
  
  std::list<double> l = { 3.1, 1.2, 4.3, 2.4, 5.5, 9.7 };
  std::cout << "min element is: " << *min_elem(std::begin(l), std::end(l), std::greater<double>()) << std::endl;
  
  Student s[] = { {30, "Curry"}, {23, "Lebron"}, {35, "Durant"} };
  std::cout << "min element is: " << *min_elem(std::begin(s), std::end(s)) << std::endl;
}
```

The above program outputs:

```cpp
min element is: 1
min element is: 9.7
min element is: Lebron23
```

### Answer

```cpp
Compare
last
first != last
smallest
typename
operator<
```

---

## 007.5

### Question

The struct Buffer is a simple container that encapsulates fixed-size arrays. Please fill in the blanks to finish its design.

```cpp
#include <iostream>
#include <stdexcept>

class BufferIndexError : public 

{

private:

  int index;

public:

  BufferIndexError(int idx) : std::out_of_range(""), index(idx) {}

  int getIndex() const { return index; }

};


template <typename T, int N>

struct Buffer

{

  int size() const

  {

                    ;

  }

  bool empty() const

  {

                      ;

  }

  const T& operator[](int i) const

  {

    if (             )

      return elems[i];

                     BufferIndexError(i);

  }

  const T& front() const

  {

                      ;

  }

  const T& back() const

  {

                      ;

  }



               elems[             ];

};





              operator<<(std::ostream &out, const Buffer<T, N> &buf)

{

  for (int i = 0; i < N; ++i)

                  ;

  return out;

}



int main()

{

  Buffer<int, 4> numbers = {1, 3, 1, 4};

  Buffer<int, 0> no_numbers;

  std::cout << "numbers.empty(): " << numbers.empty() << '\n';

  std::cout << "no_numbers.empty(): " << no_numbers.empty() << '\n';



  Buffer<char, 16> letters = {

    'D','o',' ','n','o','t',' ','a','n','s','w','e','r','!','!','!'

  };

  if (!letters.empty())

  {

    std::cout << "The first character is: " << letters.front() << '\n';

    std::cout << "The last character is: " << letters.back() << '\n';

  }

  std::cout << letters << '\n';



  

                  {

    int k = 0;

    while (true)

      std::cout << letters[k++];

  }

  

  {

    std::cout << "\nBuffer index is out of range: " << ex.() << std::endl;

  }

}
```


The above program outputs:

```bash
numbers.empty(): 0
no_numbers.empty(): 1
The first character is: D
The last character is: !
Do not answer!!!
Do not answer!!!
Buffer index is out of range: 16
```

### Answer

```cpp
#include <iostream>
#include <stdexcept> // 需要包含 <stdexcept> 以使用 std::out_of_range

// BufferIndexError 类定义，继承自 std::out_of_range
class BufferIndexError : public std::out_of_range // 填充1: 基类
{
private:
    int index;
public:
    // 构造函数，初始化基类和成员变量
    BufferIndexError(int idx) : std::out_of_range("Buffer index out of range"), index(idx) {}
    // 获取错误索引的方法
    int getIndex() const { return index; }
};

// Buffer 结构体模板定义
template <typename T, int N>
struct Buffer
{
    // 获取缓冲区大小的方法
    int size() const
    {
        return N; // 填充2: 返回模板参数 N
    }

    // 判断缓冲区是否为空的方法
    bool empty() const
    {
        return N == 0; // 填充3: 当 N 为 0 时为空
    }

    // 重载下标运算符 (const 版本)
    const T& operator[](int i) const
    {
      // 检查索引是否在有效范围内
      if (i >= 0 && i < N) // 填充4: 索引有效条件
          return elems[i];
      // 如果索引无效，则抛出自定义异常
      throw BufferIndexError(i); // 修正/填充5: 抛出异常
    }

    // 获取第一个元素的引用 (const 版本)
    const T& front() const
    {
        // 注意：更健壮的实现会检查 N > 0
        // if (empty()) throw std::out_of_range("front() called on empty buffer");
        return elems[0]; // 填充6: 返回第一个元素
    }

    // 获取最后一个元素的引用 (const 版本)
    const T& back() const
    {
        // 注意：更健壮的实现会检查 N > 0
        // if (empty()) throw std::out_of_range("back() called on empty buffer");
        return elems[N-1]; // 填充7: 返回最后一个元素
    }

    T elems[N]; // 填充8: 声明定长数组成员，类型为 T，大小为 N
};

// 重载输出流运算符，用于打印 Buffer 内容
template <typename T, int N> // 填充9: operator<< 的模板声明和返回类型
std::ostream& operator<<(std::ostream &out, const Buffer<T, N> &buf)
{
    for (int i = 0; i < N; ++i) // 使用 N 或 buf.size()
        out << buf[i]; // 填充10: 输出当前索引的元素
    return out; // 填充11: 返回输出流对象
}

int main()
{
    Buffer<int, 4> numbers = {1, 3, 1, 4};
    Buffer<int, 0> no_numbers;
    std::cout << "numbers.empty(): " << numbers.empty() << '\n';
    std::cout << "no_numbers.empty(): " << no_numbers.empty() << '\n';

    Buffer<char, 16> letters = {
        'D','o',' ','n','o','t',' ','a','n','s','w','e','r','!','!','!'
    };
    if (!letters.empty())
    {
        std::cout << "The first character is: " << letters.front() << '\n';
        std::cout << "The last character is: " << letters.back() << '\n';
    }
    std::cout << letters << '\n';

    try // 填充11: try 块开始
    {
        int k = 0;
        while (true) // 这个循环会无限执行，直到 letters[k++] 抛出异常
            std::cout << letters[k++];
    } catch (const BufferIndexError& ex) // 填充12: catch 块，捕获 BufferIndexError 类型的异常
    {
        // 输出错误信息，包括超出范围的索引值
        std::cout << "\nBuffer index is out of range: " << ex.getIndex() << std::endl; // 填充13: 调用 getIndex() 获取索引
    }
    return 0; // 良好的 main 函数应该有返回值
}
```