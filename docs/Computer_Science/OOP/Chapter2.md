---
statistics: True
comments: true
---

# Chapter 2 | A tour of cpp

```cpp
#include <iostream>

void selection_sort(int arr[], int n){
    for(int i = 0; i < n - 1; i++){
        int min_idx = 1;
        for(int j = i + 1; j < n; j++){
            if(arr[j] < arr[min_idx]){
                min_idx = j;
            }
        }
        if(min_idx != i){
            int tmp = arr[min_idx];
            arr[min_idx] = arr[i];
            arr[i] = tmp;
        }
    }
}

void print_array(int arr[], int n){
    for(int i = 0; i < n; i++) {
        std::cout << arr[i] << " ";
    }
    std::cout << std::endl;
}

int main(){
    int arr[] = {64, 25, 12, 23, 11};
    int n = sizeof(arr) / sizeof(arr[0]);

    selection_sort(arr, n);
    print_array(arr, n);

    return 0;
}

```

---

- 然后我们升级一下 `selection_sort` 函数，让它使用 `min_element` 函数来找到最小元素的下标。

```cpp
int min_element(int arr[], int begin, int end){
    int min_idx = begin;
    for(int i = begin + 1; i < end; i++){
        if(arr[i] < arr[min_idx]){
            min_idx = i;
        }
    }
    return min_idx;
}

void swap(int& a, int& b){
    int tmp = a;
    a = b;
    b = tmp;
}

void selection_sort(int arr[], int n){
    for(int i = 0; i < n - 1; i++){
        int min_idx = min_element(arr, i, n);
        if(min_idx != i){
            swap(arr[i], arr[min_idx]);
        }
    }
}
```

---

## about `int&` 

- 关于 `swap(int& a, int& b)` 函数 :

这样下面的 `a` 与 `b` 不用加 `*`， `&` 为引用。此时 `a` 和 `b` 是 `int&` 类型，即 int 的引用。

当你写 `a = b` ; 时，你实际上是在修改 `a` 所引用的原始变量的值，而不是修改 `a` 本身（因为 `a` 是一个引用，它只是另一个变量的别名）。同样，`b = tmp` ; 也是直接修改 `b` 所引用的原始变量的值。

---

- 当我们需要支持 `double` 类型的数组时，我们可以通过修改 `min_element` 函数以支持 `double` 类型。

```cpp
#include <iostream>

int min_element(double arr[], int begin, int end){
    int min_idx = begin;
    for(int i = begin + 1; i < end; i++){
        if(arr[i] < arr[min_idx]){
            min_idx = i;
        }
    }
    return min_idx;
}

void swap(double& a, double& b){
    double tmp = a;
    a = b;
    b = tmp;
}

void selection_sort(double arr[], int n){
    for(int i = 0; i < n - 1; i++){
        int min_idx = min_element(arr, i, n);
        if(min_idx != i){
            swap(arr[i], arr[min_idx]);
        }
    }
}

void print_array(double arr[], int n){
    for(int i = 0; i < n; i++) {
        std::cout << arr[i] << " ";
    }
    std::cout << std::endl;
}

int main(){
    double arr[] = {64.1, 25.3, 12.2, 23.5, 11.7};
    int n = sizeof(arr) / sizeof(arr[0]);

    selection_sort(arr, n);
    print_array(arr, n);

    return 0;
}
```

## about function overloading

C++ 中的 函数重载（Function Overloading） 是一种允许在同一作用域内定义多个同名函数的特性。这些同名函数必须满足以下条件：

1. 函数名相同。
2. 参数列表不同（参数的类型、数量或顺序不同）。
3. 返回类型可以相同也可以不同，但仅返回类型不同不足以构成重载。

在编译时，编译器会根据调用函数时提供的参数类型和数量，选择最匹配的重载函数。如果没有找到匹配的函数，编译器会报错。

- 如果函数是成员函数，`const` 修饰符可以用于区分重载函数。

```cpp
void foo() const;    // 常量成员函数
void foo();          // 非常量成员函数
```

- 默认参数不会改变函数的签名，因此不能用于区分重载函数。

```cpp
void foo(int x, int y = 10); // 合法
void foo(int x);             // 错误：与上面的函数冲突
```

---

- 至此我们发现，变动点是参数的类型，因此我们把类型变动抽出来，作为一个参数。


==T可以换成别的符号吗==

```cpp
#include <iostream>
#include <string>

template <typename T>  // T 是一个占位符，表示任意类型 
int min_element(T arr[], int begin, int end){
    int min_idx = begin;
    for(int i = begin + 1; i < end; i++){
        if(arr[i] < arr[min_idx]){
            min_idx = i;
        }
    }
    return min_idx;
}

template <typename T>
void swap(T& a, T& b){
    T tmp = a;
    a = b;
    b = tmp;
}

template <typename T>
void selection_sort(T arr[], int n){
    for(int i = 0; i < n - 1; i++){
        int min_idx = min_element(arr, i, n);
        if(min_idx != i){
            swap(arr[i], arr[min_idx]);
        }
    }
}

template <typename T>
void print_array(T arr[], int n){
    for(int i = 0; i < n; i++) {
        std::cout << arr[i] << " ";
    }
    std::cout << std::endl;
}

int main(){
    std::string arr[] = {"hello", "world", "zju", "boys", "girls"}; // 能比较是因为库里面有比较函数
    int n = sizeof(arr) / sizeof(arr[0]);

    selection_sort(arr, n);
    print_array(arr, n);

    return 0;
}
```

## about template

- 模板是泛型编程的基础。泛型编程的目的是编写与数据类型无关的代码。例如，你可以编写一个通用的排序函数，它可以对 `int、double、string` 等类型的数据进行排序，而不需要为每种类型都写一个单独的排序函数。
- **作用范围**：`template <typename T>` 的作用范围仅限于紧随其后的一个函数或一个类。如果你有多个函数或类需要使用相同的模板参数 T，你需要为每个函数或类单独声明 `template <typename T>`。

---

- 如果是自定义类型呢？

```cpp
struct Student{
    int id;
    std::string name;

    // bool operator < (const Student& s){
    //    return id < s.id;
    // }
};

bool operator < (const Student& s1, const Student& s2){
    return s1.id < s2.id;
}


std::ostream& operator << (std::ostream& out, const Student& s){
    return out << "(" << s.id << "," << s.name << ")";
}

int main(){
    Student arr[] = {{2011, "Newton"}, {2001, "Gauss"}, {2134,"Euler"}, {2067, "Riemann"}, {2054, "Mozi"}};
    int n = sizeof(arr) / sizeof(arr[0]);

    selection_sort(arr, n);
    print_array(arr, n);

    return 0;
}
```

## about 重载

- `std::ostream&` 是返回值，返回输出流对象的引用，以支持链式调用。
- `std::ostream& out` 是参数，表示传入的参数是一个输出流对象，用于输出数据。
- `const Student&` 是参数，表示传入的参数是一个常量引用，以避免不必要的拷贝，并保证传入的 `Student` 对象不会被修改。使用引用（`&`）避免拷贝对象，提高效率。

??? note "为什么将 `operator<<` 定义为全局函数？"
    `operator<<` 的第一个参数是 `std::ostream&` ，而不是 Student 对象。因此，它不能作为 Student 的成员函数，而必须定义为全局函数。

    如果定义为成员函数，调用方式会变成 `s << std::cout` ，这与常规用法相反。

??? note "attention if id and name are private"
    如果 `id` 和 `nam`e 是 Student 类的私有成员，`operator<<` 需要声明为 Student 的友元函数。

    just like this:

    ```cpp
    class Student{
    private:
        int id;
        std::string name;
    public:
        Student(int id, const std::string& name) : id(id), name(name) {}

        // 声明友元函数
        friend std::ostream& operator << (std::ostream& out, const Student& s);
    };
    ```

---

- 如果将 `operator <` 定义在 `Student` 结构体内部，它是一个成员函数。成员函数可以直接访问结构体的私有成员（如果有），并且调用时隐含了 `this` 指针。

示例 :

```cpp
struct Student {
    int id;
    std::string name;

    // 成员函数形式的 operator<
    bool operator < (const Student& s) const {
        return id < s.id;
    }
};
```

1. 隐含的 `this` 指针：

    - 在成员函数中，`id` 实际上是 `this->id` ，`s.id` 是参数对象的 `id`。例如，`a < b` 会被解释为 `a.operator<(b)`。

2. 访问权限：

    - 成员函数可以直接访问结构体的私有成员（如果有）。

- 如果将 `operator<` 定义在 `Student` 结构体外部，它是一个全局函数。全局函数需要通过参数访问结构体的成员，因此如果成员是私有的，需要将其声明为友元函数。

示例 :  

```cpp
struct Student {
    int id;
    std::string name;

    // 声明友元函数
    friend bool operator < (const Student& a, const Student& b);
};

// 全局函数形式的 operator<
bool operator < (const Student& a, const Student& b) {
    return a.id < b.id;
}
```

1. 显式参数：

    - 全局函数需要显式地传递两个参数（如 `a` 和 `b`），而不是通过 `this` 指针。

2. 访问权限：

    - 如果结构体的成员是私有的，全局函数需要被声明为友元函数（`friend`），才能访问私有成员。

3. 调用方式：

    - 通过参数调用，例如 `operator<(a, b)` 或 `a < b`。

---

```cpp
class Rectangle{
private: 
    double w, h;
    double area, perimeter;
public:
    Rectangle(double w, double h): w(w), h(h){
        // 构造函数 constructor
    }
    void calc_area(){
        area = w * h;
    }
    void calc_perimeter(){
        perimeter = 2 * (w + h);
    }
};

#include <cmath>

class Triangle{
private:
    double a, b, c;
public:
    Triangle(double a, double b, double c): a(a), b(b), c(c){ }
    void calc_area(){
        double p = (a + b + c) / 2;
        area = sqrt(p * (p - a) * (p - b) * (p - c));
    }
    void calc_perimeter(){
        perimeter = a + b + c;
    }
};

const double PI = 3.14;

class Circle{
private:
    double r;
public:
    Circle(double r): r(r){ }
    void calc_area(){
        area = PI * r * r;
    }
    void calc_perimeter(){
        perimeter = 2 * PI * r;
    }
};

int main(){
    Rectangle arr[] = {Rectangle(2,3), Rectangle(5,5)};
    Circle arr2[] = {Circle(3)};
    Triangle arr3[] = {Triangle(2,4,5)};

    int n = sizeof(arr) / sizeof(arr[0]);

    for(Rectangle& r : arr){  // range for loop 甚至可以写成 for(auto& r : arr)
        r.calc_area();
        r.calc_perimeter();
    }


    selection_sort(arr, n);
    print_array(arr, n);

    return 0;
}
```

### about for

- `for` 循环的语法 :

```cpp
for (元素类型 变量名 : 容器) {
    // 循环体
}
```

- `Rectangle& r` 是数组中每个元素的引用。使用 `Rectangle& r` 可以避免拷贝对象，直接操作数组中的元素。
- `auto` 可以由编译器根据初始化表达式自动推导出类型。

---

```cpp
class Shape{
protected:
    double area, perimeter;
public:
    virtual ~Shape() = default;
    double get_area() const { return area; }
    double get_perimeter() const { return perimeter; }
    virtual void calc_area() = 0;
    virtual void calc_perimeter() = 0;
    virtual std::string name() = 0;
    friend ostream& operator<<(ostream& , const Shape&);
};

class Circle: public Shape{
private:
    double r;
public:
    double get_area() const{ return area; }
    double get_perimeter() const{ return perimeter; }
    Circle(double r): r(r){ }
    void calc_area() override{
        area = PI * r * r;
    }
    void calc_perimeter() override{
        perimeter = 2 * PI * r;
    }
    void name() const override{
        return "Circle";
    }
};

std::ostream& operator<<(std::ostream& os, const Shape& s){
    return out << "(" << s.name << ":" << s.area << ", " << s.perimeter << ")";
}


template <typename T>
void print_array(T* arr[], int n){
    for(int i = 0; i < n; i++){
        cout << *arr[i] << " ";
    }
    std::cout << std::endl;
}

template <typename T, typename Compare>
int min_element(T arr[], int begin, int end, Compare comp){
    int min_idx = begin;

    for(int i = begin + 1; i < end; i++){
        if(comp(arr[i], arr[min_idx])){
            min_idx = i;
        }
    }
    return min_idx;
}

bool less_shape_area(Shape* s1, Shape* s2){
    return s1->get_area() < s2->get_area();
}

template <typename T, typename Compare>
void selection_sort(T arr[], int n, Compare comp){
    for(int i = 0; i < n - 1; i++){
        int min_idx = min_element(arr, i, n, comp);
        if(min_idx != i){
            swap(arr[i], arr[min_idx]);
        }
    }
}

int main(){
    Shape arr[] = {Circle(3)}; 
    Shape *arr[] = {new Rectangle(2,3), new Rectangle(5,5), new Circle(3), new Triangle(2,4,5)}; 
    int n = sizeof(arr) / sizeof(arr[0]);

    for(Shape* s : arr){
        s->calc_area();
        s->calc_perimeter();
    }

    selection_sort(arr, n, less_shape_area);
    selection_sort(arr, n, [](Shape* s1, Shape* s2){return s1->get_area() < s2->get_area();}); 
    print_array(arr, n);

    return 0;
}
```

## about encapsulation(封装)

- `private` : 指用户不能直接访问，例如在 `Rectangle` 中不能用 `Rectangle.w` 来访问
- `class` 默认是 private

---

## about 析构函数

- 析构函数（Destructor） 是 C++ 中的一种特殊成员函数，用于在对象销毁时执行清理操作。它的主要作用是释放对象在生命周期内分配的资源（如动态内存、文件句柄、网络连接等），避免资源泄漏。
- 析构函数是类的成员函数，名称与类名相同，前面加上 `~`，没有返回类型，也没有参数。
- 当对象的生命周期结束时，析构函数会自动调用。

1. 动态内存管理
    
    如果类中使用了动态内存分配（如 new），需要在析构函数中释放内存（如 delete）。

```cpp
class MyClass {
private:
    int* data;
public:
    MyClass(int size) {
        data = new int[size];  // 动态分配内存
    }

    ~MyClass() {
        delete[] data;  // 释放内存
    }
};
```

2. 确保资源释放

    即使程序发生异常，析构函数也会被调用，确保资源被正确释放。

3. 虚析构函数

    虚析构函数的主要目的是确保在通过基类指针删除派生类对象时，能够正确调用派生类的析构函数。如果没有虚析构函数，可能会导致派生类的析构函数不被调用，从而引发资源泄漏或其他未定义行为。

    ```cpp
    class Base {
    public:
        ~Base() {
            std::cout << "Base destructor called!" << std::endl;
        }
    };

    class Derived : public Base {
    public:
        ~Derived() {
            std::cout << "Derived destructor called!" << std::endl;
        }
    };

    int main() {
        Base* ptr = new Derived();  // 基类指针指向派生类对象
        delete ptr;  // 只调用 Base 的析构函数，Derived 的析构函数不会被调用！
        return 0;
    }
    ```

    输出 :

    ```cpp
    Base destructor called!
    ```

    由于 `Base` 的析构函数不是虚函数，`delete ptr` 只会调用 `Base` 的析构函数，而不会调用 `Derived` 的析构函数。

    因此需要 :

    ```cpp
    class Base {
    public:
        virtual ~Base() {  // 虚析构函数
            std::cout << "Base destructor called!" << std::endl;
        }
    };

    class Derived : public Base {
    public:
        ~Derived() {
            std::cout << "Derived destructor called!" << std::endl;
        }
    };

    int main() {
        Base* ptr = new Derived();  // 基类指针指向派生类对象
        delete ptr;  // 正确调用 Derived 和 Base 的析构函数
        return 0;
    }
    ```

    输出 :

    ```cpp
    Derived destructor called!
    Base destructor called!
    ```

    因此，虚析构函数通过虚表机制，确保在运行时正确调用派生类的析构函数。如果类可能被继承，且基类指针可能指向派生类对象，应将基类的析构函数声明为虚函数。

    - 使用 `= default` 可以避免手动实现空的析构函数，保持代码简洁和一致性。

---

## about `override`

- `override` 关键字用于明确表示一个成员函数是重写基类的虚函数。如果函数标记为 `override`，但基类中没有对应的虚函数，编译器会报错。
- `override` 关键字可以省略。只要函数签名与基类的虚函数匹配，编译器就会认为这是重写。
- 然而，如果函数签名与基类的虚函数不匹配（例如拼写错误或参数类型不同），编译器不会报错，而是认为这是一个新的函数。这可能导致程序行为不符合预期，且难以调试。

---

## about const

```cpp
std::ostream& operator<<(std::ostream& os, const Shape& s){
    return out << "(" << s.name << ":" << s.area << ", " << s.perimeter << ")";
}
```

此处必须要加上 `const` ，因为在 `Shape` 里面存在

```cpp
void name() const override{
    return "Circle";
}
```

**const 对象和 const 成员函数**

- 如果一个对象是 `const` 的（如 `const Shape& s`），只能调用它的 `const` 成员函数。
- 如果一个成员函数没有标记为 `const`，编译器会认为它可能修改对象的状态，因此不允许在 `const` 对象上调用。

---

## about slicing

```cpp
Shape arr[] = {Circle(3)}; 
Shape *arr[] = {new Rectangle(2,3), new Rectangle(5,5), new Circle(3), new Triangle(2,4,5)}; 
```

- **对象切片**是指将派生类对象赋值给基类对象时，派生类对象的特有部分（即派生类新增的成员变量和函数）会被"切掉"，只保留基类部分。这是因为基类对象没有足够的内存空间来存储派生类的额外数据。
- `Shape* arr[]` 是一个指针数组，每个元素都是 `Shape*` 类型的指针。由于指针可以指向派生类对象，因此可以存储不同类型的对象（如 `Rectangle`、`Circle`、`Triangle` 等）。

---

## about `lambda`

```cpp
selection_sort(arr, n, [](Shape* s1, Shape* s2){return s1->get_area() < s2->get_area();});
```

Lambda 表达式的基本语法如下：

```cpp
[捕获列表](参数列表) -> 返回类型 { 函数体 }
```

- **捕获列表**：用于捕获外部变量，可以是值捕获、引用捕获或隐式捕获。
- **参数列表**：与普通函数的参数列表类似。
- **返回类型**：可以省略，编译器会自动推导。
- **函数体**：Lambda 表达式的实现代码。

示例 :

```cpp
auto lambda = [](int x, int y) -> bool { return x < y; };
bool result = lambda(3, 5);  // 调用 Lambda 表达式
```

### Lambda 表达式的灵活性

- Lambda 表达式可以通过捕获列表访问外部变量：

1. 值捕获：[x, y]，捕获外部变量的值。
2. 引用捕获：[&x, &y]，捕获外部变量的引用。
3. 隐式捕获：[=]（值捕获所有变量）或 [&]（引用捕获所有变量）。

```cpp
int threshold = 10;
auto lambda = [threshold](Shape* s) { return s->get_area() > threshold; };
```

- Lambda 表达式可以直接作为函数参数传递，使代码更简洁。

---