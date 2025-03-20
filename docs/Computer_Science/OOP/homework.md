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