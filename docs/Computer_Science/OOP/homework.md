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