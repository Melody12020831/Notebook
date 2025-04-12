---
statistics: True
comments: true
---

# Chapter 7 | Polymorphism

## More on constructors

```cpp
#include <iostream>
using namespace std;

struct Base{
public:
    Base (int i) : data(i) {cout << "Base::Base()" << endl;}
    ~Base() {cout << "Base::~Base()" << endl;}
    void print() {cout << "Base::print():" << data << endl;}
protected:
    void setdata(int i) {data = i;}
private:
    int data;
};

class C{
public:
    C(int i) {cout << "C::C()" << endl;}
    ~C() {cout << "C::~C()" << endl;}
}

struct Derived : public Base{
public:
    Derived(): c(20), Base(10) {
        cout << "Derived::Derived()" << endl;
    }
    ~Derived() {cout << "Derived::~Derived()" << endl;}

private:
    C c;
};

int main(){
    Derived d;
}
```

输出：

```bash
Base::Base()
C::C()
Derived::Derived()
Derived::~Derived()
C::~C()
Base::~Base()
```

---

- Base class is always constructed first.
- If no explicit arguments are passed to base class, the default constructor will be called.
- Destructors are called in exactly the reverse order of the constructors.

---

### Name hiding

- If you redefine a member function in the derived class, all the other overloaded functions in the base class are inaccessible.
- We'll see how the keyword virtual affects function overloading next time.

---

### class vs. struct

- `class` defaults to `private`
- `struct` defaults to `public`

---

### Access protection： `friend`

- Grant access explicitly
- The class itself controls the access
- A friend can be:
    - a free function
    - a member function of another classo or even an entire class

```cpp
struct X;

struct Y{
    void f(X*);
};

struct X{
private:
    int i;
public:
    void initialize();
    friend void g(X*, int); // global friend
    friend void h();
    friend void Y::f(X*); // struct member friend
    friend struct Z; // entire struct friend
};

void X::initialize(){
    i = 0;
}

void g(X* x, int i){
    x->i = i;
}

void h(){
    X x;
    x.i = 100; // Direct data manipulation
}

void Y::f(X* x){
    x->i = 47;
}

struct Z{
private:
    int j;
public:
    void initialize();
    void g(X* x);
};

void Z::initialize(){
    j = 99;
}

void Z::g(X* x){
    x->i += j;
};

int main(){
    X x;
    Z z;
}
```

- 一般来说很少用到 `friend` 关键字，除了例如 operators overloading 的时候，会用到 `friend` 关键字。

---

### Access protection： `private` 

- `private` is to class, not to object
- A secret detour:
    - `private members can be accessed
    - indirect read/write by pointers

```cpp
#include <iostream>
using namespace std;

struct Base{
public:
    Base (int i) : data(i) {cout << "Base::Base()" << endl;}
    ~Base() {cout << "Base::~Base()" << endl;}
    void print() {cout << "Base::print():" << data << endl;}
    void foo(Base *other) {cout << "Base::foo(), other -> data = " << other->data << endl;}
protected:
    void setdata(int i) {data = i;}
private:
    int data;
};

int main(){
    Base b1(11), b2(12);
    b1.foo(&b2);
}
```

- `private` 的访问权限是基于类（class）的，而不是基于对象（instance）的。
- 在 `foo()` 内部，通过 `other->data` 访问 `b2` 的私有成员 `data` ，这属于类内部的合法访问。

---

```cpp
#include <iostream>
using namespace std;

struct Base{
public:
    int data;
    Base() : data(10) {}
};

struct Derived : public Base{  
private:
    int i;
public:
    Derived() : i(30) {}
    void printi() {cout << "Derived::i = " << i << endl;}
};

int main(){
    Base b;
    Derived d;
    
    cout << b.data << ", " << d.data << endl;  // 10, 10
    cout << sizeof(b) << ", " << sizeof(d) << endl;  // 4, 8

    int *p = (int*)&b;
    cout << *p << ", " << *p << endl; // 0xd438fff8e4, 10

    p = (int*)&d;
    cout << *p << ", " << *p << endl; // 0xd438fff8e0, 10

    *p = 200;
    cout << d.data << endl;  // 200

    d.printi();  // Derived::i = 30

    p++;
    cout << *p << ", " << *p << endl; // 0xd438fff8e4
    *p = 50;
    d.printi();  // Derived::i = 50
}
```

- 尽管 `i` 是私有字段，但是还是在外面被改掉了

---

### Access protection

- Inheritance

```cpp
class Derived1 : public Base {}
class Derived2 : protected Base {}
class Derived3 : private Base {}
```

- 三个关键词在继承时也可以用

---

#### How inheritance affects access

- Suppose class B is derived from class A.

|inheritance type (B is)|public members|protected members|private members|
|:---|:---|:---|:---|
|: private A|private in B|private in B|not accessible|
|: protected A|protected in B|protected in B|not accessible|
|: public A|public in B|protected in B|not accessible|

---

### Conversions

- Public Inheritance should imply substitution:
    - If B is-a A, you can use a B anywhere an A can be used.
    - if B is-a A, then everything that is true for A is also true of B.
    - [Liskov’s Substitution Principle](https://en.wikipedia.org/wiki/Liskov_substitution_principle)

---

## Upcasting

- Regard an object of the derived class as an object of the base class
    - only valid for reference or pointer.

---

### Upcasting examples

```cpp
Manager pete("Pete", "444-55-6666", "Bakery");
Employee * ep = &pete; // Upcast
Employee & er = pete; // Upcast
```

- Lose type information about the object:

```cpp
ep->print(cout); // base class version of print
```

- 如果想要在打印时依旧保留 Manager 的信息，这就需要用到多态了。

---

## Polymorphism

### Virtual destructors

- Make destructors virtual if they might be inherited

```cpp
Shape *p = new Ellipse(100.0F, 200.0F);
...
delete p; // which dtor?
```

- `Shape::~Shape()` is invoked if not virtual!
- Want `Ellipse::~Ellipse()` to be called:
    - Must declare `virtual Shape::~Shape()` , which is implicitly called inside `Ellipse::~Ellipse()` .

```cpp
#include <iostream>
using namespace std;

class Shape{
public:
    void move(){
        cout << "Shape::move()" << endl;
    }
    virtual void render(){
        cout << "Shape::render()" << endl;
    }
};

class Ellipse : public Shape{
public:
    void render(){
        cout << "Ellipse::render()" << endl;
    }
};

class Circle : public Ellipse{
public:
    void render(){
        cout << "Circle::render()" << endl;
    }
};

void foo(Shape *p){
    p->move();
    p->render();
}

int main(){
    Ellipse e;
    Circle c;
    foo(&e);
    foo(&c);
}
```

- 如果没有用 `virtual` 关键字，那么输出将会是：

```bash
Shape::move()
Shape::render()
Shape::move()
Shape::render()
```

- 如果加上 `virtual` 关键字，那么输出将会是：

```bash
Shape::move()
Ellipse::render()
Shape::move()
Circle::render()
```

---

```cpp
#include <iostream>
#include <vector>
using namespace std;

class Shape{
public:
    virtual ~Shape() {};
    void move(){
        cout << "Shape::move()" << endl;
    }
    virtual void render(){
        cout << "Shape::render()" << endl;
    }
};

class Ellipse : public Shape{
public:
    ~Ellipse(){
        cout << "Ellipse::~Ellipse()" << endl;
    }
    void render(){
        cout << "Ellipse::render()" << endl;
    }
};

class Circle : public Ellipse{
public:
    ~Circle(){
        cout << "Circle::~Circle()" << endl;
    }
    void render(){
        cout << "Circle::render()" << endl;
    }
};

void foo(Shape *p){
    p->move();
    p->render();
}

void move_and_render(std::vector<Shape*> &shapes){
    for(auto p : shapes){
        foo(p);
    }
}

int main(){
    std::vector<Shape*> all_shapes;
    all_shapes.push_back(new Circle);
    all_shapes.push_back(new Ellipse);
    
    move_and_render(all_shapes);

    delete all_shapes[0];
    delete all_shapes[1];
}
```

输出：

```bash
Shape::move()
Circle::render()
Shape::move()
Ellipse::render()
```

- delete 时会发现这两者的析构函数没有被调用。
- 这是因为，在 C++ 中，析构函数默认是**非虚函数**，这意味着它们不会自动地被派生类重写。因此，当使用基类指针删除派生类对象时，只会调用基类的析构函数，而不会调用派生类的析构函数。这可能会导致资源泄漏或其他问题。
- 此时需要给 Shape 加上一个 `virtual ~Shape() {}`，这样在 delete 时就会调用派生类的析构函数了。此时的输出是：

```bash
Shape::move()
Circle::render()
Shape::move()
Ellipse::render()
Circle::~Circle()
Ellipse::~Ellipse()
Ellipse::~Ellipse()
```

- 这里会有两个 `Ellipse::~Ellipse()`，这是因为 Circle 是继承自 Ellipse 的，所以 Circle 的析构函数会先调用 Ellipse 的析构函数，然后再调用自己的析构函数。
- 如果是给 Shape 加上 `virtual ~Shape() = 0;`，就会报错。
- 原因是当派生类对象被销毁时，会隐式调用基类的析构函数。如果基类的纯虚析构函数没有实现，链接器将无法找到其定义，导致编译错误。因为 Shape 的纯虚析构函数只有声明，没有实现。

---

```cpp
#include <iostream>
using namespace std;

class Base{
public:
    Base() : data(10) {}
    void foo() { cout << "Base::foo(): data = " << data << endl; }
private:
    int data;
};

int main(){
    Base b;
    b.foo();

    cout << "size of b is: " << sizeof(b) << endl;
}

输出：

```bash
Base::foo(): data = 10
size of b is: 4
```

---

- 接着加入一个 `bar()` 函数

```cpp
#include <iostream>
using namespace std;

class Base{
public:
    Base() : data(10) {}
    void foo() { cout << "Base::foo(): data = " << data << endl; }
    virtual void bar() { cout << "Base::bar()" << endl; }
private:
    int data;
};

int main(){
    Base b;
    b.foo();
    b.bar();

    cout << "size of b is: " << sizeof(b) << endl;

    int *p = (int *)&b;
    cout << *p << endl;
    p++;
    cout << *p << endl;
    p++;
    cout << *p << endl;
}
```

输出：

```bash
Base::foo(): data = 10
Base::bar()
size of b is: 16
58290032
32758
10
```

```plain
|------------------|
| vptr (8 bytes)   |  // 虚函数表指针
|------------------|
| data (4 bytes)   |  // int data = 10
| padding (4 bytes)|  // 填充对齐
|------------------|
```

**操作分析：**

1. `&b` 获取对象起始地址（指向 `vptr`）。
2. `(int *)&b` 将地址强制转换为 `int*`，此时 `p` 指向 `vptr` 的首 4 字节。
3. `(void**)p` 将 `p` 转换为 `void**`，即指向 `void*` 的指针，此时 `pp` 指向 `vptr` 的起始位置。
4. `*pp` 解引用获取 `vptr` 的值（即虚函数表的地址）。

- 指针的加减操作是基于**指针类型的大小**进行偏移的。
    - 若 `p` 是 `int*` 类型，`p += 1` 会将指针移动 `sizeof(int)` 字节（通常 4 字节）。
    - 若 `p` 是 `char*` 类型，`p += 1` 仅移动 1 字节。

- Shape 的析构函数做成 virtual 之后，派生类的析构函数会与基类析构函数形成覆盖关系。
    - 当基类的析构函数被声明为 virtual 时，编译器会为该类生成一个虚函数表，表中记录了虚函数的地址。
    - 派生类的析构函数会隐式继承基类的虚析构函数属性，并自动成为虚函数（即使未显式添加 virtual 关键字）。
    - 此时，派生类析构函数在虚函数表中覆盖了基类析构函数的入口地址。
    - 销毁时的动态绑定
        - 当通过基类指针删除派生类对象时，编译器通过虚函数表找到实际对象类型对应的析构函数。
        - 调用顺序为：派生类析构函数 $\rightarrow$ 基类析构函数（自底向上）。

---

- 其实 10 前面的八个字节是一个指针指向外面

```cpp
#include <iostream>
using namespace std;

class Base{
public:
    Base() : data(10) {}
    void foo() { cout << "Base::foo(): data = " << data << endl; }
    virtual void bar() { cout << "Base::bar()" << endl; }
private:
    int data;
};

int main(){
    Base b;
    b.foo();
    b.bar0();

    cout << "size of b is: " << sizeof(b) << endl;

    int *p = (int *)&b; // 将对象地址强制转换为 int*
    void* *pp = (void* *)p; // 再转换为 void**（等价于指向虚函数表的指针）
    void* vptr = *pp; // 获取虚函数表地址
    cout << vptr << endl; // 输出虚函数表地址
    p += 2;
    cout << *p << endl;

    Base b2;
    void *vptr2 = *((void**)&b2);

    cout << (void*)main << endl;
    cout << vptr << endl;
    cout << vptr2 << endl;
}
```

输出：

```bash
Base::foo(): data = 10
Base::bar()
size of b is: 16
0x7ff6a9d46f70
10
0x7ff6a9c81540
0x7ff6a9d46f70
0x7ff6a9d46f70
```

- 可以看到其实比较接近。所以其实是一个代码段的东西。

---

```cpp
#include <iostream>
using namespace std;

class Base{
public:
    Base() : data(10) {}
    void foo() { cout << "Base::foo(): data = " << data << endl; }
    virtual void bar0() { cout << "Base::bar0()" << endl; }
    virtual void bar1() { cout << "Base::bar1()" << endl; }
private:
    int data;
};

class Derived : public Base{
public:
    void bar0() { cout << "Derived::bar0()" << endl; }
    void bar1() { cout << "Derived::bar1()" << endl; }
};

int main(){
    Base b;
    b.foo();

    cout << "size of b is: " << sizeof(b) << endl;

    int *p = (int *)&b;
    void* *pp = (void* *)p;
    void* vptr = *pp;
    cout << vptr << endl;
    p += 2;
    cout << *p << endl;

    Base b2;
    void *vptr2 = *((void**)&b2);
    cout << vptr2 << endl;

    Derived d;
    void *vptrd = *((void**)&d);
    cout << vptrd << endl;

    void* *vfuncs = (void* *)vptr;
    void* f0 = vfuncs[0];
    cout << "f0:" << f0 << endl;
    void* f1 = vfuncs[1];
    cout << "f1:" << f1 << endl;

    void* *vfuncsd = (void* *)vptrd;
    void* f0d = vfuncsd[0];
    cout << "f0d:" << f0d << endl;
    void* f1d = vfuncsd[1];
    cout << "f1d:" << f1d << endl;

    cout << "f0 == f0d: " << ((f0 == f0d) ? "True" : "False") << endl;
    cout << "f1 == f1d: " << ((f1 == f1d) ? "True" : "False") << endl;
}
```

输出：

```bash
Base::foo(): data = 10
size of b is: 16
0x7ff66b866ff0
10
0x7ff66b866ff0
0x7ff66b867010
f0:0x7ff66b7c25a0
f1:0x7ff66b7c25e0
f0d:0x7ff66b7c2680
f1d:0x7ff66b7c26c0
f0 == f0d: False
f1 == f1d: False
```

- 因为每个类（包含虚函数或继承自包含虚函数的类）会生成一个唯一的虚函数表。基类和派生类的虚函数表是独立的。

**Base 类的虚函数表**

```plain
|------------------|
| &Base::bar0()    |  // 第一个虚函数地址
|------------------|
| &Base::bar1()    |  // 第二个虚函数地址
|------------------|
```

**Derived 类的虚函数表**

```plain
|---------------------|
| &Derived::bar0()    |  // 覆盖基类的 bar0()
|---------------------|
| &Derived::bar1()    |  // 覆盖基类的 bar1()
|---------------------|
```

- 若派生类未重写虚函数，地址会相同：

```cpp
class Derived : public Base {
    // 不重写 bar0() 和 bar1()
};
```

此时输出：

```bash
f0 == f0d: True
f1 == f1d: True
```

---

```cpp
#include <iostream>
using namespace std;

class Base{
public:
    Base() : data(10) {}
    void foo() { cout << "Base::foo(): data = " << data << endl; }
    virtual void bar0() { cout << "Base::bar0()" << endl; }
    virtual void bar1() { cout << "Base::bar1()" << endl; }
private:
    int data;
};

class Derived : public Base{
public:
    void bar0() { cout << "Derived::bar0()" << endl; }
    void bar1(int a) { cout << "Derived::bar1(int): datad + a = " << datad + a << endl; }
private:
    int datad;
};

int main(){
    Base b;
    b.foo();

    cout << "size of b is: " << sizeof(b) << endl;

    int *p = (int *)&b;
    void* *pp = (void* *)p;
    void* vptr = *pp;
    cout << vptr << endl;
    p += 2;
    cout << *p << endl;

    Base b2;
    void *vptr2 = *((void**)&b2);
    cout << vptr2 << endl;

    Derived d;
    void *vptrd = *((void**)&d);
    cout << vptrd << endl;

    void* *vfuncs = (void* *)vptr;
    void* f0 = vfuncs[0];
    cout << "f0:" << f0 << endl;
    void* f1 = vfuncs[1];
    cout << "f1:" << f1 << endl;

    void* *vfuncsd = (void* *)vptrd;
    void* f0d = vfuncsd[0];
    cout << "f0d:" << f0d << endl;
    void* f1d = vfuncsd[1];
    cout << "f1d:" << f1d << endl;

    cout << "f0 == f0d: " << ((f0 == f0d) ? "True" : "False") << endl;
    cout << "f1 == f1d: " << ((f1 == f1d) ? "True" : "False") << endl;
}
```

输出：

```bash
Base::foo(): data = 10
size of b is: 16
0x7ff77a256ff0
10
0x7ff77a256ff0
0x7ff77a257010
f0:0x7ff77a1b2630
f1:0x7ff77a1b2670
f0d:0x7ff77a1b2710
f1d:0x7ff77a1b2670
f0 == f0d: False
f1 == f1d: True
```

- 派生类要覆盖基类的虚函数，必须满足函数签名完全一致（包括参数类型、数量、const 修饰符等）。
- `Derived::bar1(int)` 的签名与 `Base::bar1()` 不匹配，因此它不会覆盖基类的虚函数，而是成为派生类中的一个新函数（与基类虚函数共存）。
- 其实是要用 `override` 但是在上述签名不同的情况下，编译器会报错。

---

### 多态实现的流程

1. 声明虚函数

在基类中用 `virtual` 关键字声明需要多态行为的函数。

2. 生成虚函数表（vtable）

- 编译器为每个包含虚函数的类生成一个虚函数表。
- `vtable` 按声明顺序存储该类所有虚函数的地址。

3. 分配虚表指针（vptr）

- 每个对象实例隐式包含一个指向其所属类 vtable 的指针（vptr）。
- 对象构造时，vptr 被初始化为指向当前类的 vtable。

4. 派生类覆盖虚函数

- 派生类重写（override）基类虚函数时，其 vtable 中对应条目替换为派生类函数的地址。

5. 动态绑定

通过基类指针/引用调用虚函数时：

    - 通过对象的 vptr 找到对应的 vtable。
    - 根据函数声明顺序，从 vtable 中取出目标函数的地址。
    - 调用该地址的函数（实际指向派生类实现）。

---

```cpp
#include <iostream>
using namespace std;

class Base{
public:
    Base() : data(10) {}
    void foo() { cout << "Base::foo(): data = " << data << endl; }
    virtual void bar0() { cout << "Base::bar0()" << endl; }
    virtual void bar1(int) { cout << "Base::bar1(int)" << endl; }
private:
    int data;
};

class Derived : public Base{
public:
    void bar0() { cout << "Derived::bar0()" << endl; }
    void bar1(int a) { cout << "Derived::bar1(int): datad + a = " << datad + a << endl; }
private:
    int datad;
};

int main(){
    Base b;
    b.foo();

    cout << "size of b is: " << sizeof(b) << endl;

    int *p = (int *)&b;
    void* *pp = (void* *)p;
    void* vptr = *pp;
    cout << vptr << endl;
    p += 2;
    cout << *p << endl;

    Base b2;
    void *vptr2 = *((void**)&b2);
    cout << vptr2 << endl;

    Derived d;
    void *vptrd = *((void**)&d);
    cout << vptrd << endl;

    void* *vfuncs = (void* *)vptr;
    void* f0 = vfuncs[0];
    cout << "f0:" << f0 << endl;
    void* f1 = vfuncs[1];
    cout << "f1:" << f1 << endl;

    void* *vfuncsd = (void* *)vptrd;
    void* f0d = vfuncsd[0];
    cout << "f0d:" << f0d << endl;
    void* f1d = vfuncsd[1];
    cout << "f1d:" << f1d << endl;

    cout << "f0 == f0d: " << ((f0 == f0d) ? "True" : "False") << endl;
    cout << "f1 == f1d: " << ((f1 == f1d) ? "True" : "False") << endl;

    void (*vf)(Derived*, int) = (void (*)(Derived*, int))f1d;
    vf(&d, 20);
}
```

输出：

```bash
Base::foo(): data = 10
size of b is: 16
0x7ff649c17010
10
0x7ff649c17010
0x7ff649c17030
f0:0x7ff649b72650
f1:0x7ff649b72690
f0d:0x7ff649b72730
f1d:0x7ff649b72770
f0 == f0d: False
f1 == f1d: False
Derived::bar1(int): datad + a = 20
```

- `Derived::bar1(int)` 是类的非静态成员函数，其调用需要隐式的 `this` 指针。
- 如果是 `void (*vf)(int)` 则会导致编译错误，因为 `vf` 是一个普通函数指针，而不是成员函数指针。
- 实际上成员函数指针的类型应为 `void (Derived::*)(int)`。

---

### What happens if

```cpp
Ellipse elly(20f, 40f);
Circle circ(60f);
elly = circ;
```

- Area of `circ` is sliced off
    - only the part of `circ` fits in `elly` gets copied
- The `vptr` from `circ` is ignored
    - `vptr` in `elly` still points to the `Ellipse vtable`

---

```cpp
#include <iostream>
using namespace std;

class Base {
public:
    Base() : data(10) {}
    virtual void bar() { cout << "Base::bar(): data = " << data << endl; }
protected:
    int data;
};

class Derived : public Base {
public:
    Derived() : datad(100) {data = 7;} 
    void bar() override { cout << "Derived::bar(): data = " << data << ", datad = " << datad << endl; }
private:
    int datad;
};

int main(){
    Base b;
    b.bar();  // 静态绑定

    Derived d;
    Base *p = &d;
    p->bar();  // 动态绑定

    b = d;
    b.bar();
    p = &b;
    p->bar();
}
```

输出:

```bash
Base::bar(): data = 10
Derived::bar(): data = 7, datad = 100
Base::bar(): data = 7
Base::bar(): data = 7
```

- 将 `Derived` 对象 `d` 赋值给 `Base` 对象 `b` 时，只会复制 `Base` 部分的成员（`data = 7`），`Derived` 特有的成员（`datad`）被丢弃。
- 此时**静态绑定** `b` 仍然是 `Base` 类型对象，调用 `Base::bar()`，输出修改后的 `data = 7`。
- **动态绑定但无多态**，虽然通过指针调用虚函数，但 `p` 此时指向的是 `Base` 对象 `b`，因此调用 `Base::bar()`。data 仍为 7（上一步赋值后的值）。
- 可以看出赋值之后，这个 `b` 对象的 `vptr` 指向的是 `Base` 的虚函数表，而不是 `Derived` 的虚函数表。说明，赋值操作不会改变 `vptr` 的指向。

---

#### 如果进行人为地更改 `vptr`

```cpp
#include <iostream>
using namespace std;

class Base {
public:
    Base() : data(10) {}
    virtual void bar() { cout << "Base::bar(): data = " << data << endl; }
protected:
    int data;
};

class Derived : public Base {
public:
    Derived() : datad(100) {data = 7;} 
    void bar() override { cout << "Derived::bar(): data = " << data << ", datad = " << datad << endl; }
private:
    int datad;
};

int main(){
    Base b;
    b.bar();  // 静态绑定

    Derived d;
    Base *p = &d;
    p->bar();  // 动态绑定

    b = d;

    void* *pb = (void* *)&b;
    void* *pd = (void* *)&d;
    *pb = *pd;

    b.bar();
    p = &b;
    p->bar();
}
```

输出:

```bash
Base::bar(): data = 10
Derived::bar(): data = 7, datad = 100
Base::bar(): data = 7
Derived::bar(): data = 7, datad = 32759
```

- 因为 `b` 是一个 `Base` 对象，所以 `b.bar()` 仍然是静态绑定，可以确定是 `Base` 类型的，所以会调用 `Base::bar()`。
- 因为 `vptr` 被 copy 过，此时指向的是 `Derived` 的虚函数表。
- 但是此时 `datad` 的值是 `b` 的 `data` 值再下面，也就是由 `b` 的存`vptr` 的地方加上偏移量算出来的内存中一个未知的值。

---

#### private v.s. protected

|特性|private|protected|
|:---:|:---:|:---:|
|本类内部|✔️ 可访问|✔️ 可访问|
|派生类|❌ 不可访问|✔️ 可访问|
|友元函数/类|✔️ 可访问|✔️ 可访问|
|外部代码|❌ 不可访问|❌ 不可访问|
|典型用途|隐藏实现细节|为派生类提供扩展接口|

- 优先使用 `private`：遵循最小暴露原则，减少耦合。
- 谨慎使用 `protected`：仅在明确需要派生类扩展时使用，避免过度暴露内部逻辑。

---

### What happens with pointers?

```cpp
Ellipse *elly = new Ellipse(20f, 40f);
Circle *circ = new Circle(60f);
elly = circ;
```

- Well, the original `Ellipse` for `elly` is lost...
    - 如果不 `delete` 则会造成内存泄漏
- `elly` and `circ` point to the same `Circle` object!
    - `elly->render(); // Circle::render()`

---

### Virtual and reference arguments

```cpp
void func(Ellipse& elly) {
    elly.render();
}
Circle circ(60F);
func(circ);
```

- References act like pointers
- `Circle::render()` is called

---

### Calls up the chain

- You can still call the overridden function for reuse

```cpp
void Derived::func() {
    cout << "In Derived::func()!";
    Base::func(); // call to base class
}
```

- This is a common way to add new functionality
- No need to copy the old stuff!
- 这个 function 也可以是 virtual 的。
- 在 `Base::func()` 中就不是动态绑定了，而是静态绑定了。

---

### 动态绑定 v.s. 静态绑定

- **静态绑定**：编译时确定，高效但缺乏多态支持。

- **动态绑定**：运行时确定，通过虚函数实现多态，是面向对象的核心特性之一。

```cpp
Derived d;
d.func();           // 静态绑定（直接通过对象调用）
Base& ref = d;     
ref.func();         // 动态绑定（通过引用调用虚函数）
Base* ptr = &d;    
ptr->func();        // 动态绑定（通过指针调用虚函数）
```

---

#### 动态绑定的触发条件

必须同时满足：

1. 通过指针或引用调用：直接通过对象实例调用时，即使函数是虚函数，也使用静态绑定。
2. 调用虚函数：非虚函数不参与动态绑定。

---

## Relaxation example

```cpp
class Expr {
public:
    virtual Expr* newExpr();
    virtual Expr& clone();
    virtual Expr self();
};
class BinaryExpr : public Expr {
public:
    virtual BinaryExpr* newExpr(); // ok
    virtual BinaryExpr& clone(); // ok
    virtual BinaryExpr self(); // Error!
};
```

### **协变返回类型是什么？**

- **定义**：当派生类重写基类虚函数时，如果基类函数的返回类型是**基类指针/引用**，派生类可以将返回类型改为**派生类指针/引用**。

### **为什么要使用协变返回类型？**

1. **类型安全**：避免强制类型转换，直接返回具体类型的指针/引用。
2. **代码简洁性**：无需手动向下转型（`dynamic_cast`），减少错误。
3. **多态支持**：保持接口统一，同时允许实现细节差异。

- 在C++中，虚函数的重写需要满足严格的**协变返回类型（covariant return type）**规则。
- **协变返回类型**允许派生类重写虚函数时，返回类型可以是基类返回类型的**派生类**，但需满足：
  - 返回类型为 **指针** 或 **引用**。
  - 派生类的返回类型与基类的返回类型具有继承关系（即 `BinaryExpr` 是 `Expr` 的子类）。
- 协变返回类型仅适用于 **指针或引用**，而 `self()` 返回的是对象（值类型）。
- 此时，派生类必须严格保持返回类型与基类一致（即 `Expr`），否则视为函数签名不同，导致重写失败。
- **实际行为**：
  - `BinaryExpr self()` 会被视为一个新的虚函数，而非对基类 `Expr self()` 的重写。
  - 编译器会报错：函数签名不一致（返回类型不兼容）。

- 可改写为:

```cpp
// 基类修改
virtual Expr* self();  // 或 virtual Expr& self();

// 派生类重写
virtual BinaryExpr* self() override;  // 或 virtual BinaryExpr& self() override;
```

### **关键规则**

1. **协变返回类型**：
   - 只允许指针或引用。
   - 派生类返回类型必须是基类返回类型的直接或间接子类。

2. **对象返回类型**：
   - 重写时返回类型必须与基类严格一致。
   - 若不一致，视为函数签名不同，导致重写失败。


---

### **示例：克隆模式**

- **基类定义**

```cpp
class Animal {
public:
    virtual Animal* clone() {  // 返回基类指针
        return new Animal(*this);
    }
};
```

- **派生类重写**

```cpp
class Dog : public Animal {
public:
    virtual Dog* clone() override {  // 协变返回类型：返回派生类指针
        return new Dog(*this);
    }
};
```

- **使用场景**

```cpp
Dog* myDog = new Dog();
Animal* animalPtr = myDog;          // 基类指针指向派生类对象

Dog* clonedDog = animalPtr->clone(); // 直接得到Dog*，无需强制转换
```

---

## Example interface

```cpp
class CDevice {
public:
    virtual ~CDevice() {}
    virtual int read(...) = 0;
    virtual int write(...) = 0;
    virtual int open(...) = 0;
    virtual int close(...) = 0;
    virtual int ioctl(...) = 0;
}
```

- 这样的接口类里面是没有变量的，只有程序的函数。
- 接口类不会有多重继承的问题，因为接口类里面没有数据存储。
- 可以定义很多接口类，然后通过多重继承各种接口。

---

## Further reading

<div class="card file-block" markdown="1">
<div class="file-icon"><img src="/Notebook/assets/images/pdf.svg" style="height: 3em;"></div>
<div class="file-body">
<div class="file-title"> Design Patterns - Abstract Factory </div>
<div class="file-meta"> 552 KB / 2025-04-01</div>
</div>
<a class="down-button" target="_blank" href="/Notebook/Computer_Science/OOP/Further_reading/[Further Readings] Design Patterns - Abstract Factory.pdf" markdown="1">:fontawesome-solid-download: 下载</a>
</div>

---