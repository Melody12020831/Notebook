---
statistics: True
comments: true
---

# Chapter 8 | Design

## Newton's method

- Just a few iterations

$x_{n+1} = x_n - \frac{f(x_n)}{f'(x_n)}$

e.g. $f(x) = x^2 - 2, f'(x) = 2x$

```cpp
#include <iostream>
#include <cmath>

int main(){
    int k = 0;
    double x = 1.0;
    std::cout << "k = " << k << ", x = " << x << std::endl;

    while((std::fabs(x * x - 2) > 1e-12) && (k++ < 30)){
        x = x - (x * x - 2) / (2 * x);
        std::cout << "k = " << k << ", x = " << x << std::endl;
    }
}
```

输出：

```
k = 0, x = 1
k = 1, x = 1.5
k = 2, x = 1.41667
k = 3, x = 1.41422
k = 4, x = 1.41421
k = 5, x = 1.41421
```

- `cout` 输出的时候默认是 `6` 位小数。

---

### 改成参数为 `a` 的函数：

```cpp
#include <iostream>
#include <cmath>

int main(){
    double a = 2;
    double tolerance = 1e-12;
    int max_iter = 30;

    int k = 0;
    double x = 1.0;
    std::cout << "k = " << k << ", x = " << x << std::endl;

    while((std::fabs(x * x - a) > tolerance) && (k++ < max_iter)){
        x = x - (x * x - a) / (2 * x);
        std::cout << "k = " << k << ", x = " << x << std::endl;
    }
}
```

---

### 接下来做一个封装

```cpp
#include <iostream>
#include <cmath>

class NewtonSolver{
private:
    double a;
    double tolerance;
    int max_iter;
    int k;
    double x;
public:
    NewtonSolver(double a, double tolerance, int max_iter): a(a), tolerance(tolerance), max_iter(max_iter){
    }
    void print_info(){
        std::cout << "k = " << k << ", x = " << x << std::endl;
    }
    double f(double x){
        return x * x - a;
    }
    double df(double x){
        return 2 * x;
    }
    bool is_close(double x){
        return std::fabs(f(x)) < tolerance;
    }
    void improve(double x0){
        k = 0;
        x = x0;
        print_info();
        
        while(!is_close(x) && (k++ < max_iter)){
            x = x - (f(x)) / (df(x));
            print_info();
        }
    }
};
int main(){
    NewtonSolver solver(2, 1e-6, 100);
    solver.improve(1.0);
    return 0;
}
```

---

### 更加抽象的封装

- 对于 OOP 来说，要做得更抽象，也即更关注牛顿迭代法本身的逻辑

```cpp
#include <iostream>
#include <cmath>

class NewtonSolver{
private:
    double tolerance;
    int max_iter;
    int k;
    double x;
public:
    NewtonSolver(double tolerance = 1e-12, int max_iter=30): tolerance(tolerance), max_iter(max_iter){
    }
    void improve(double x0){
        k = 0;
        x = x0;
        print_info();
        
        while(!is_close(x) && (k++ < max_iter)){
            x = x - (f(x)) / (df(x));
            print_info();
        }
    }
private: 
    // implement the following functions for your problem.
    virtual double f(double x) = 0;
    virtual double df(double x) = 0;

    void print_info(){
        std::cout << "k = " << k << ", x = " << x << ", f(x) = " << f(x) << std::endl;
    }
    bool is_close(double x){
        return std::fabs(f(x)) < tolerance;
    }
    
};

class SqrtSolver: public NewtonSolver{
private:
    double a;
public:
    SqrtSolver(double a): a(a){
    }
private:
    double f(double x) override{
        return x * x - a;
    }
    double df(double x) override{
        return 2 * x;
    }
};

int main(){
    SqrtSolver solver(612.0);
    solver.improve(1.0);
    return 0;
}
```

输出:

```bash
k = 0, x = 1, f(x) = -611
k = 1, x = 306.5, f(x) = 93330.2        
k = 2, x = 154.248, f(x) = 23180.6      
k = 3, x = 79.108, f(x) = 5646.08       
k = 4, x = 43.4221, f(x) = 1273.48      
k = 5, x = 28.7582, f(x) = 215.032      
k = 6, x = 25.0195, f(x) = 13.9773      
k = 7, x = 24.7402, f(x) = 0.0780241    
k = 8, x = 24.7386, f(x) = 2.48651e-06  
k = 9, x = 24.7386, f(x) = 1.13687e-13
```

??? note "如果基类构造参数无默认值"
    那么，派生类必须显式传递基类参数。

    ```cpp
    SqrtSolver(double a) : NewtonSolver(1e-12, 30), a(a) {}
    ```

!!! note "about 纯虚函数"
    在C++中，函数可以声明为纯虚函数的场景如下：

    1. **定义接口规范**  
    当基类需要定义一个通用接口，强制所有派生类必须实现该函数时，可将函数声明为纯虚。例如，设计一个形状基类`Shape`时，其计算面积的`area()`方法应为纯虚函数，因为不同子类（如`Circle`、`Rectangle`）需各自实现具体逻辑。

    2. **基类无法提供默认实现**  
    若基类无法给出合理的默认实现，而必须由子类根据自身特性实现，应使用纯虚函数。例如，动物基类`Animal`的`speak()`方法，不同动物叫声不同，基类无法统一实现。

    3. **强制抽象类**  
    若希望类无法被实例化（只能作为基类），可为其添加至少一个纯虚函数。例如，抽象类`AbstractDevice`声明纯虚函数`initialize()`，确保所有设备子类必须实现初始化逻辑。

    4. **接口类设计**  
    当类仅用于定义接口（类似Java的`interface`），所有方法均可设为纯虚。例如，`IReadable`接口声明纯虚的`read()`方法，强制实现类提供读取功能。

    **注意事项**：
    
    - **纯虚函数可实现**：C++允许纯虚函数有实现（需在类外定义），但子类仍必须覆盖它。基类实现可通过`Base::function()`在子类中调用。
    - **析构函数特殊处理**：若声明纯虚析构函数，必须提供实现（否则导致链接错误）。例如：

    ```cpp
    class AbstractBase {
    public:
        virtual ~AbstractBase() = 0; // 声明为纯虚
    };
    AbstractBase::~AbstractBase() {} // 必须提供定义
    ```

    **何时不宜使用纯虚函数？**

    - **基类能提供合理默认实现**：若基类方法有通用逻辑，子类可选择是否覆盖，应使用普通虚函数而非纯虚。
    - **非多态需求**：若无需运行时多态，或类直接实例化有意义，则无需纯虚函数。

---

### 添加n方根

```cpp
#include <iostream>
#include <cmath>

class NewtonSolver{
private:
    double tolerance;
    int max_iter;
    int k;
    double x;
public:
    NewtonSolver(double tolerance = 1e-12, int max_iter=30): tolerance(tolerance), max_iter(max_iter){
    }
    void improve(double x0){
        k = 0;
        x = x0;
        print_info();
        
        while(!is_close(x) && (k++ < max_iter)){
            x = x - (f(x)) / (df(x));
            print_info();
        }
    }
private: 
    // implement the following functions for your problem.
    virtual double f(double x) = 0;
    virtual double df(double x) = 0;

    void print_info(){
        std::cout << "k = " << k << ", x = " << x << ", f(x) = " << f(x) << std::endl;
    }
    bool is_close(double x){
        return std::fabs(f(x)) < tolerance;
    }
    
};

class SqrtSolver: public NewtonSolver{
private:
    double a;
public:
    SqrtSolver(double a): a(a){
    }
private:
    double f(double x) override{
        return x * x - a;
    }
    double df(double x) override{
        return 2 * x;
    }
};

// f(x) = x^n - a
// df(x) = n*x^(n-1)

class NthRootSolver: public NewtonSolver{
private:
    double a;
    int n;
public:
    NthRootSolver(double a, int n): a(a), n(n){
    }
private:
    double f(double x) override{
        return std::pow(x, n) - a;
    }
    double df(double x) override{
        return n * std::pow(x, n-1);
    }
};

int main(){
    NthRootSolver solver(64.0, 2);
    solver.improve(1.0);
    return 0;
}
```

输出:

```bash
k = 0, x = 1, f(x) = -63
k = 1, x = 32.5, f(x) = 992.25
k = 2, x = 17.2346, f(x) = 233.032
k = 3, x = 10.474, f(x) = 45.7054
k = 4, x = 8.29219, f(x) = 4.76044
k = 5, x = 8.00515, f(x) = 0.0823941
k = 6, x = 8, f(x) = 2.64846e-05
k = 7, x = 8, f(x) = 2.72848e-12
k = 8, x = 8, f(x) = 0
```

---

### 再添加三角函数

```cpp
#include <iostream>
#include <cmath>

class NewtonSolver{
private:
    double tolerance;
    int max_iter;
    int k;
    double x;
public:
    NewtonSolver(double tolerance = 1e-12, int max_iter=30): tolerance(tolerance), max_iter(max_iter){
    }
    void improve(double x0){
        k = 0;
        x = x0;
        print_info();
        
        while(!is_close(x) && (k++ < max_iter)){
            x = x - (f(x)) / (df(x));
            print_info();
        }
    }
private: 
    // implement the following functions for your problem.
    virtual double f(double x) = 0;
    virtual double df(double x) = 0;

    void print_info(){
        std::cout << "k = " << k << ", x = " << x << ", f(x) = " << f(x) << std::endl;
    }
    bool is_close(double x){
        return std::fabs(f(x)) < tolerance;
    }
    
};

class SqrtSolver: public NewtonSolver{
private:
    double a;
public:
    SqrtSolver(double a): a(a){
    }
private:
    double f(double x) override{
        return x * x - a;
    }
    double df(double x) override{
        return 2 * x;
    }
};

// f(x) = x^n - a
// df(x) = n*x^(n-1)

class NthRootSolver: public NewtonSolver{
private:
    double a;
    int n;
public:
    NthRootSolver(double a, int n): a(a), n(n){
    }
private:
    double f(double x) override{
        return std::pow(x, n) - a;
    }
    double df(double x) override{
        return n * std::pow(x, n-1);
    }
};

// f(x) = cos(x) - x^3
// df(x) = -sin(x) - 3x^2

class CosSolver: public NewtonSolver{
private:
    double f(double x) override{
        return std::cos(x) - std::pow(x, 3);
    }
    double df(double x) override{
        return -std::sin(x) - 3 * std::pow(x, 2);
    }
};

int main(){
    CosSolver solver;
    solver.improve(1.0);
    return 0;
}
```

输出:

```bash
k = 0, x = 1, f(x) = -0.459698
k = 1, x = 0.880333, f(x) = -0.0453512
k = 2, x = 0.865684, f(x) = -0.000632313
k = 3, x = 0.865474, f(x) = -1.2892e-07
k = 4, x = 0.865474, f(x) = -5.21805e-15
```

---

### 抽象有很多种做法

```cpp
#include <iostream>
#include <cmath>
#include <functional>
using fn = std::function<double(double)>;

void print_info(int k, double x, double fx){
    std::cout << "k = " << k << ", x = " << x << ", f(x) = " << fx << std::endl;
}

bool is_close(double fx, double tolerance){
    return std::fabs(fx) < tolerance;
}

double newton_solve(fn f, fn df, double x0, double tolerance=1e-12, int max_iter=30){
    int k = 0;
    double x = x0;
    print_info(k, x, f(x));
    
    while(!is_close(f(x), tolerance) && (k++ < max_iter)){
        x = x - (f(x)) / (df(x));
        print_info(k, x, f(x));
    }
    return x;
}

double sqrt_newton(double a, double x0 = 1.0){
    auto f = [a](double x){ return x * x - a; };
    auto df = [](double x){ return 2 * x; };
    return newton_solve(f, df, x0);
}

double nth_root_newton(double a, int n, double x0 = 1.0){
    auto f = [a, n](double x){ return std::pow(x, n) - a; };
    auto df = [n](double x){ return n * std::pow(x, n - 1); };
    return newton_solve(f, df, x0);
}

double cos_newton(double x0 = 1.0){
    auto f = [](double x){ return std::cos(x) - std::pow(x, 3); };
    auto df = [](double x){ return -std::sin(x) - 3 * std::pow(x, 2); };
    return newton_solve(f, df, x0);
}

int main(){
    sqrt_newton(2.0);
    nth_root_newton(64, 6);
    cos_newton();
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
k = 0, x = 1, f(x) = -63
k = 1, x = 11.5, f(x) = 2.313e+06
k = 2, x = 9.58339, f(x) = 774601
k = 3, x = 7.98629, f(x) = 259395
k = 4, x = 6.65557, f(x) = 86854.2
k = 5, x = 5.54712, f(x) = 29070.5
k = 6, x = 4.62463, f(x) = 9718.82
k = 7, x = 3.8589, f(x) = 3238.05
k = 8, x = 3.22822, f(x) = 1067.82
k = 9, x = 2.72061, f(x) = 341.503
k = 10, x = 2.33874, f(x) = 99.6394
k = 11, x = 2.1014, f(x) = 22.1086
k = 12, x = 2.01147, f(x) = 2.23449
k = 13, x = 2.00016, f(x) = 0.0311752
k = 14, x = 2, f(x) = 6.32365e-06
k = 15, x = 2, f(x) = 2.55795e-13
k = 0, x = 1, f(x) = -0.459698
k = 1, x = 0.880333, f(x) = -0.0453512
k = 2, x = 0.865684, f(x) = -0.000632313
k = 3, x = 0.865474, f(x) = -1.2892e-07
k = 4, x = 0.865474, f(x) = -5.21805e-15
```

- `std::function<double(double)>` 表示一个接受 `double` 类型参数并返回 `double` 类型的可调用对象。通过 `fn` 别名，后续可以直接用 `fn` 代替冗长的 `std::function<double(double)>`，使代码更简洁。
- `f` 通过 `[a]` 捕获外部的 `a`，确保在方程中使用正确的目标值。
- 通过 `fn` 类型：允许传入 任意形式的可调用对象（如 `Lambda`、普通函数、类成员函数等），而不仅限于特定类型。可以统一处理函数指针。

---

## Further reading

<div class="card file-block" markdown="1">
<div class="file-icon"><img src="/Notebook/assets/images/pdf.svg" style="height: 3em;"></div>
<div class="file-body">
<div class="file-title"> Design Patterns - Observer </div>
<div class="file-meta"> 603 KB / 2025-04-07</div>
</div>
<a class="down-button" target="_blank" href="/Notebook/Computer_Science/OOP/Further_reading/[Further Readings] Design Patterns - Observer.pdf" markdown="1">:fontawesome-solid-download: 下载</a>
</div>

<div class="card file-block" markdown="1">
<div class="file-icon"><img src="/Notebook/assets/images/pdf.svg" style="height: 3em;"></div>
<div class="file-body">
<div class="file-title"> Software Engineering__CH-12.3 </div>
<div class="file-meta"> 471 KB / 2025-04-07</div>
</div>
<a class="down-button" target="_blank" href="/Notebook/Computer_Science/OOP/Further_reading/[Further Readings] Software Engineering__CH-12.3.pdf" markdown="1">:fontawesome-solid-download: 下载</a>
</div>

---