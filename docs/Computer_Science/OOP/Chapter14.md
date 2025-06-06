---
statistics: True
comments: true
---

# Chapter 14 | Smart Pointers

## Standard smart pointers

Standard library holder for raw pointers

- `std::unique_ptr`
- `std::shared_ptr`
- `std::weak_ptr`
- `std::auto_ptr` (deprecated in C++11)

---

### Put them all together

- Templates
- Inheritance
- Reference Counting
- eSmart Pointers

```
C++ Strategies and Tactics, Robert Murray,1993
```

??? note "Garbage Collection"
    垃圾回收机制是一种自动化的内存管理技术。在支持垃圾回收的编程语言中，程序员不需要手动分配和释放内存。运行时环境会自动检测不再被程序使用的内存（即"垃圾"），并将其回收以便重新利用。

    C++ 本身并没有内置的垃圾回收机制。这是因为 C++ 的设计哲学是提供对硬件的底层控制和最大的性能。C++ 采用了手动内存管理的方式，程序员使用 `new` 来分配内存，使用 `delete` 来释放内存。这种方式提供了高度的灵活性和性能，但也带来了内存泄漏（忘记释放不再使用的内存）和野指针（指向已释放内存的指针）等风险。

    虽然 C++ 标准本身没有垃圾回收，但可以使用智能指针（如 `std::unique_ptr` 和 `std::shared_ptr`）来帮助管理内存，它们通过 RAII（Resource Acquisition Is Initialization）原则，在对象超出作用域时自动释放其管理的资源，从而减少手动内存管理的负担和错误。此外，也有第三方库为 C++ 提供了垃圾回收的功能，但这些不是标准 C++ 的一部分。

??? note "RAII"
    RAII 的全称是 Resource Acquisition Is Initialization，中文可以理解为资源获取即初始化。这是一种在 C++ 中（以及其他一些具有确定性对象生命周期的语言中）用于管理资源的编程技术，这些资源包括内存、文件句柄、网络套接字或锁等等。

    RAII 的核心思想是将资源的生命周期与对象的生命周期绑定在一起。

    它的工作原理如下：
    
    1. 资源获取： 在对象的构造函数中获取资源。如果资源获取失败，构造函数应该抛出异常。
    2. 初始化： 现在对象负责管理这个资源。
    3. 资源释放： 当对象被销毁时（无论是超出作用域、被显式删除，还是因为异常），析构函数会自动释放资源。
    
    这种方法保证了无论对象生命周期如何结束（正常退出作用域、函数返回或异常发生），资源都会被释放。这有助于防止资源泄露。
    
    智能指针，比如 std::unique_ptr 和 std::shared_ptr，就是 RAII 的典型例子。它们在构造函数中获取内存，并在对象超出作用域时，通过析构函数自动释放内存（调用 delete）。

在 C++ 中，当你使用 `new` 来动态地在堆上分配一块内存时，你需要负责在不再需要这块内存时使用 `delete` 手动释放它。如果忘记 `delete`，就会导致内存泄露。

智能指针（比如 unique_ptr 和 shared_ptr）通过 RAII 的机制，自动在它们所指向的对象不再需要时（通常是智能指针对象超出作用域时）调用 `delete` 来释放内存。这样，程序员就不需要手动去记住什么时候调用 delete，从而大大简化了内存管理，减少了内存泄露的风险。

也就是说使用智能指针可以简化管理。

- 手动管理

```cpp
#include <iostream>
#include <memory>
using namespace std;

struct Resource {
    int data;
    Resource(int d = 0) : data(d) {}
    ~Resource() {
        cout << "Resource destroyed: " << endl;
    }
};

int main(){
    {   
        Resource *p = new Resource;
        delete p;
    }
}
```

- 而智能指针可以简化这个事情

```cpp
#include <iostream>
#include <memory>
using namespace std;

struct Resource {
    int data;
    Resource(int d = 0) : data(d) {}
    ~Resource() {
        cout << "Resource destroyed" << endl;
    }
};

int main(){
    {
        // unique_ptr<Resource> p = new Resource; ERROR!
        unique_ptr<Resource> p(new Resource);
    }
    cout << "\nbefore quit ... " << endl;
}
```

输出：

```bash
Resource destroyed

before quit ...
```

- 智能指针**不能隐式转换**。

??? note "原因"
    智能指针（尤其是 `std::unique_ptr` 和 `std::shared_ptr`）不支持隐式转换，主要是为了**避免资源管理上的陷阱和错误**，例如双重释放（double deletion）和悬垂指针（dangling pointer）。

    1.  **所有权语义（Ownership Semantics）：**

        - `std::unique_ptr` 表示独占所有权，同一个原始指针不能被多个 `unique_ptr` 管理。如果允许隐式转换，比如将一个原始指针隐式转换为 `unique_ptr`，或者在 `unique_ptr` 之间进行隐式赋值或复制，可能会导致多个 `unique_ptr` 认为自己拥有同一个资源，最终在析构时尝试多次释放同一块内存，导致程序崩溃或未定义行为。
        - `std::shared_ptr` 表示共享所有权，但它的共享是通过引用计数来管理的。隐式转换可能会绕过引用计数的正确更新，导致计数不准确，进而引发过早释放或内存泄露。

    2.  **防止双重释放（Preventing Double Deletion）：** 这是最关键的原因。考虑以下场景（如果允许隐式转换）：

        ```cpp
        Resource* raw_ptr = new Resource(10);
        unique_ptr<Resource> p1 = raw_ptr; // 假设这里允许隐式转换
        unique_ptr<Resource> p2 = raw_ptr; // 再次隐式转换同一个原始指针
        ```

        当 p1 和 p2 超出作用域时，它们都会尝试 delete raw_ptr 指向的内存，导致双重释放错误。
        
        为了防止这种情况，`unique_ptr` 的构造函数和赋值运算符被设计为 `explicit` 或禁止拷贝。你需要显式地使用 `std::move` 来转移所有权，或者使用合适的构造函数来创建智能指针。

    3.  **明确意图（Explicit Intent）：** 不允许隐式转换迫使程序员显式地表达他们的意图。当你在使用原始指针或在不同类型的智能指针之间转换时，你需要清楚地知道自己在做什么，以及所有权是如何转移或共享的。这种显式性提高了代码的可读性和安全性。

    4.  **避免悬垂指针（Avoiding Dangling Pointers）：** 隐式转换也可能更容易产生悬垂指针。例如，如果一个原始指针被用于创建一个智能指针，而原始指针本身没有被置空，那么原始指针就可能变成一个悬垂指针，因为它指向的内存可能会在智能指针释放资源后被回收。智能指针的设计就是为了避免这种情况。

- 而 `p` 这个东西也可以去使用。

```cpp
#include <iostream>
#include <memory>
using namespace std;

struct Resource {
    int data;
    Resource(int d = 0) : data(d) {}
    ~Resource() {
        cout << "Resource destroyed" << endl;
    }
};

int main(){
    {
        unique_ptr<Resource> p(new Resource);
        cout << "p->data = " << p->data << endl;
    }
    cout << "\nbefore quit ... " << endl;
}
```

输出：

```bash
p->data = 0
Resource destroyed

before quit ...
```

- `std::unique_ptr` 禁止拷贝。
- `std::unique_ptr` 指向并管理着一块动态分配的内存资源。在任何时刻，都只能有一个 `std::unique_ptr` 指向并"拥有"这个资源。当这个 `std::unique_ptr`被销毁时（例如，离开了它所在的作用域 {}），它会自动释放其所管理的资源。
- 如果允许拷贝，那么 `p1` 和 `p2` 将会指向同一块内存地址。现在我们就有两个 `unique_ptr` 声称自己拥有同一个资源。这就直接违反了"独占"的原则。
- 这样能够从根本上杜绝"双重释放"这种严重错误的发生。它通过在编译层面就阻止你写出这样的代码，来保证内存管理的绝对安全。

```cpp
#include <iostream>
#include <memory>
using namespace std;

struct Resource {
    int data;
    Resource(int d = 0) : data(d) {}
    ~Resource() {
        cout << "Resource destroyed" << endl;
    }
};

int main(){
    {
        unique_ptr<Resource> p1(new Resource);
        unique_ptr<Resource> p2(new Resource(7));
        cout << "p->data = " << p->data << endl;

        // p1 = p2; 这个不被允许
    }
    cout << "\nbefore quit ... " << endl;
}
```

- `std::unique_ptr` 虽然禁止拷贝，但它允许移动 ( `move` )。移动操作符 std::move 可以将资源的所有权从一个 unique_ptr 转移给另一个。

```cpp
#include <iostream>
#include <memory>
using namespace std;

struct Resource {
    int data;
    Resource(int d = 0) : data(d) {}
    ~Resource() {
        cout << "Resource destroyed, data = " << data << endl;
    }
};

int main(){
    {
        cout << "--- before move ---" << endl;
        unique_ptr<Resource> p1(new Resource);
        unique_ptr<Resource> p2(new Resource(7));
        cout << "p1 = " << p1.get() << endl;
        cout << "p1->data = " << p1->data << endl;
        cout << "p2 = " << p2.get() << endl;
        cout << "p2->data = " << p2->data << endl;

        p1 = std::move(p2);

        cout << "--- after move ---" << endl;
        cout << "p1 = " << p1.get() << endl;
        cout << "p1->data = " << p1->data << endl;
        cout << "p2 = " << p2.get() << endl;
        cout << "p2->data = " << p2->data << endl;
    }
    cout << "\nbefore quit ... " << endl;
}
```

- p1 和 p2 是 `std::unique_ptr<Resource>` 类型的对象。`std::unique_ptr` 是一个类模板，它封装了一个裸指针（raw pointer），并提供了自动内存管理等功能。对于裸指针，它用于解引用指针并访问所指向对象的成员。例如，`raw_ptr->member` 等价于 `(*raw_ptr).member`。对于 `unique_ptr` 对象本身的成员（如 `get()`），使用点操作符 (`.`)。当你希望访问 `unique_ptr` 所指向的对象的成员时（如 `data`），使用箭头操作符 (`->`)。`unique_ptr` 通过重载 `operator->()` 使得这种访问看起来就像直接操作裸指针一样自然，同时它仍然在背后管理着资源。
- p1 指向新的资源就被 destroy 了（因为没人管）
- 移交出去后 p2 变成了 nullptr 
- 因为 `cout << "p2->data = " << p2->data << endl;` 会导致 segmentation fault
- `move` 就是管理权的移交。

??? note "about move"
    `std::move` 本身并不执行任何移动操作。它是一个类型转换函数（具体来说，是一个 `static_cast` 到右值引用的转换）。它的作用是告诉编译器："你可以把这个对象看作是一个临时的、可以被'窃取'资源的对象。"

    当你对一个对象 `obj` 使用 `std::move(obj)` 时：

    1. `std::move(obj)` 返回一个指向` obj` 的右值引用 (rvalue reference)。

    2. 这个右值引用告诉编译器，`obj` 的资源可以被安全地转移走，因为我们（程序员）显式地表明了这一点，暗示 `obj` 之后可能不再以其原有状态被使用，或者其状态不再重要。

    实际的移动操作是由移动构造函数 (`move constructor`) 或移动赋值运算符 (`move assignment operator`) 完成的。这些特殊的成员函数会以右值引用作为参数。

    移动构造函数 `ClassName(ClassName&& other`): 从 `other` 对象窃取资源来构造新对象。`other` 对象通常会被置为一个有效的、但可能是空或未定义的状态。
    
    移动赋值运算符 `ClassName& operator=(ClassName&& other)`: 释放当前对象的资源，然后从 `other` 对象窃取资源。`other` 对象同样会被置为一个有效的、但可能是空或未定义的状态。

??? note "about Rvalue Reference"
    左值 (Lvalue - Locator value): 指的是**表达式结束后依然存在的对象或函数**。它们通常有**持久的内存地址**，你可以获取它们的地址（使用 `&` 操作符）。可以出现在赋值操作符 (`=`) 的左边或右边。
    

    - **右值 (Rvalue - Read value / Right-hand-side value):**指的是**表达式结束后就不再存在的临时值**。它们通常没有持久的内存地址（或者说，你通常不能安全地获取它们的地址并长期使用）。只能出现在赋值操作符 (`=`) 的右边（作为提供值的一方）。
    
    **区分小技巧：** 一个简单的（但不完全精确）判断方法是：如果能对表达式取地址 (`&`)，那它通常是左值；否则，它通常是右值。

    1. **左值引用 (`Type&`)**:通常只能绑定到左值。主要作用是作为对象的别名，避免了指针的复杂语法，并常用于函数参数传递以避免复制。

    2. **右值引用 (Rvalue Reference - `Type&&`)**

    C++11 引入了**右值引用**，其主要目的是：

    1.  **实现移动语义 (Move Semantics):** 这是最核心的目的。
    2.  **实现完美转发 (Perfect Forwarding):** 在模板编程中非常有用。

    **定义和特点：**

    - **语法：** 使用两个 `&` 符号，即 `Type&&`。
    - **绑定规则：** 右值引用**专门用于绑定到右值**（临时对象）。
    - **核心作用：** 允许我们**识别出临时对象**，并安全地"窃取"它们的资源（比如动态分配的内存、文件句柄等），而不是进行昂贵的复制操作。因为临时对象即将被销毁，所以转移其资源是安全的。

    **`std::move` 和右值引用：**

    `std::move` 是一个实用函数，它并不执行任何"移动"操作。它的作用是将一个左值**无条件地转换为右值引用**。这相当于告诉编译器："你可以把这个左值当作一个临时对象（右值）来处理了，我允许你窃取它的资源。"

```cpp
#include <iostream>
#include <memory>
using namespace std;

struct Resource {
    int data;
    Resource(int d = 0) : data(d) {}
    ~Resource() {
        cout << "Resource destroyed, data = " << data << endl;
    }
};

template<typename T>
class u_ptr{
public:  // 如果使用关键字 class 来定义一个类，其成员的默认访问权限是 private。
    explicit u_ptr(T* ptr = nullptr) : p_(ptr) {}
    ~u_ptr() {
        delete p_;
    }

    // copy is prohibited
    u_ptr(const u_ptr&) = delete;
    u_ptr& operator=(const u_ptr&) = delete;

    // move is allowed
    u_ptr(u_ptr&& other) noexcept : p_(other.release()) {} 
    u_ptr& operator=(u_ptr&& other) noexcept {  // move 会找到这个版本
        reset(other.release());  // reset？这是要干什么？
        return *this;
    }

    u_ptr& operator=(u_ptr&& other) noexcept {
        if (this != &other) {
            delete p_;
        }
    }

    T& operator*() const {  // 这里为什么是 T&
        return *p_;
    }

    T* operator->() const {  // 这里为什么是 T* 如果是对象就进行这个操作，相当于是一个递归的操作
        return p_;
    }

    T* get() const {
        return p_;  // 与 operator 的区别在哪里
    }

    T* release() {
        T* ptr = p_;
        p_ = nullptr;  // 释放管理权，返回裸指针，交出管理权
        return ptr;
    }
    void reset(T* ptr = nullptr) {  // 重置管理权
        delete p_;
        p_ = ptr;
    }

private:
    T* p_;
};

int main(){
    {
        cout << "--- before move ---" << endl;
        u_ptr<Resource> p1(new Resource);
        u_ptr<Resource> p2(new Resource(7));
        cout << "p1 = " << p1.get() << endl;
        cout << "p1->data = " << p1->data << endl;
        cout << "p2 = " << p2.get() << endl;
        cout << "p2->data = " << p2->data << endl;

        p1 = std::move(p2);

        cout << "--- after move ---" << endl;
        cout << "p1 = " << p1.get() << endl;
        cout << "p1->data = " << p1->data << endl;
        cout << "p2 = " << p2.get() << endl;
        // cout << "p2->data = " << p2->data << endl;
    }
    cout << "\nbefore quit ... " << endl;
}
```

- `= delete;` : 这是一种 C++11 的特性，用于显式地告诉编译器不要为这个函数生成默认实现，并禁止任何代码调用它。如果尝试调用一个被 `= delete` 的函数，编译器会报错。

- 不是单个对象而是数组

```cpp
#include <iostream>
#include <memory>
using namespace std;

struct Resource {
    int data;
    Resource(int d = 0) : data(d) {}
    ~Resource() {
        cout << "Resource destroyed, data = " << data << endl;
    }
};

template<typename T>
class u_ptr{
public:
    explicit u_ptr(T* ptr = nullptr) : p_(ptr) {}
    ~u_ptr() {
        delete p_;
    }

    // copy is prohibited
    u_ptr(const u_ptr&) = delete;
    u_ptr& operator=(const u_ptr&) = delete;

    // move is allowed
    u_ptr(u_ptr&& other) noexcept : p_(other.release()) {}
    u_ptr& operator=(u_ptr&& other) noexcept {
        reset(other.release());
        return *this;
    }

    T& operator*() const {
        return *p_;
    }

    T* operator->() const {
        return p_;
    }

    T* get() const {
        return p_;
    }

    T* release() {
        T* ptr = p_;
        p_ = nullptr;  // 释放管理权，返回裸指针，交出管理权
        return ptr;
    }

    void reset(T* ptr = nullptr) {  // 重置管理权
        delete p_; // 先删除旧的
        p_ = ptr; // 再接管新的
    }

private:
    T* p_;
};

int main(){
    {
        cout << "--- before move ---" << endl;
        u_ptr<Resource> p1(new Resource);
        u_ptr<Resource> p2(new Resource(7));
        cout << "p1 = " << p1.get() << endl;
        cout << "p1->data = " << p1->data << endl;
        cout << "p2 = " << p2.get() << endl;
        cout << "p2->data = " << p2->data << endl;

        p1 = std::move(p2);

        cout << "--- after move ---" << endl;
        cout << "p1 = " << p1.get() << endl;
        cout << "p1->data = " << p1->data << endl;
        cout << "p2 = " << p2.get() << endl;
        // cout << "p2->data = " << p2->data << endl;
    }
    {
        unique_ptr<Resource[]> parr(new Resource[10]);
        cout << "\n Resource data = [ ";
        for(int i = 0; i < 10; ++i){
            cout << parr[i].data << " ";  // 本来就可以做，unique包了一层之后依然可以做
        }
        cout << "]" << endl;
    }
    cout << "\nbefore quit ... " << endl;
}
```

- 输出:

```bash
--- before move ---
p1 = 0x1b3c4714970
p1->data = 0
p2 = 0x1b3c47149b0
p2->data = 7
Resource destroyed, data = 0
--- after move ---
p1 = 0x1b3c47149b0
p1->data = 7
p2 = 0
Resource destroyed, data = 7

before quit ...
```

- `reset(...)`: `reset` 成员函数的作用是首先，`delete` 当前 `u_ptr` 对象（即 `*this`）所拥有的旧指针 `p_`（如果它不为 `nullptr` 的话），释放旧资源。然后，让当前 `u_ptr` 对象接管新的指针（即从 `other.release()` 返回的指针）。所以，`reset(other.release())` 这一行代码完整地实现了所有权的转移，当前对象释放旧资源，然后接管从 `other` 对象那里"偷"来的新资源。
- `T& operator*() const` : `operator*()` (解引用操作符) 的目的是提供对 `u_ptr` 所管理的实际对象的访问，就像使用裸指针一样。返回 `T&` (引用) 意味着你得到的是实际对象本身的一个别名，而不是它的一份拷贝。这允许你读取或修改所管理的对象（如果 `T` 本身不是 `const` 的话）。如果返回 `T` (按值返回)，那么每次解引用都会创建一个对象的拷贝，这不仅效率低下，而且也违背了指针解引用的通常语义（即直接操作指向的对象）。`const` 关键字在这里表示这个成员函数不会修改 `u_ptr` 对象本身（即不会改变 `p_` 指针的值），但它返回的引用所指向的对象是否能被修改，则取决于 `T` 的类型。
- `T* operator->() const` : `operator->()` (箭头操作符) 使得智能指针可以像裸指针一样通过 `->` 访问其所管理对象的成员。C++ 对重载的 `operator->()` 有一个特殊规则：它必须返回一个裸指针，或者返回一个另一个也重载了 `operator->()` 的对象。编译器会自动重复调用 `operator->()` 直到获得一个裸指针，然后通过这个裸指针访问成员。在这里，`u_ptr` 直接管理一个 `T*` 类型的裸指针 `p_`，所以最直接和正确的方式就是返回这个 `p_`。相当于是一个递归的操作，但更准确的说是链式调用 (chaining)。如果 `operator->()` 返回的是另一个也重载了 `operator->()` 的智能指针类型，编译器会继续对返回的对象调用 `operator->()`，直到最终获得一个裸指针。
- `T* get() const` 与 `operator` 的区别在于 : 是一个普通的成员函数。它显式地返回内部存储的裸指针 `p_`。`operator->()`: 是一个重载的操作符。它也返回内部存储的裸指针 `p_` (或者可以链式调用的对象)。它使得 `u_ptr` 对象可以模仿裸指针的语法来访问成员：`p1->member`。
- 对于这个 `unique_ptr<Resource[]> parr(new Resource[10]);` ，我们的版本 `u_ptr` 还不能实现，因为还没实现数组的版本，还需要增加。

```cpp
#include <iostream>
#include <memory>
using namespace std;

struct Resource {
    int data;
    Resource(int d = 0) : data(d) {}
    ~Resource() {
        cout << "Resource destroyed, data = " << data << endl;
    }
};

template<typename T>
class u_ptr{
public:
    explicit u_ptr(T* ptr = nullptr) : p_(ptr) {}
    ~u_ptr() {
        delete p_;
    }

    // copy is prohibited
    u_ptr(const u_ptr&) = delete;
    u_ptr& operator=(const u_ptr&) = delete;

    // move is allowed
    u_ptr(u_ptr&& other) noexcept : p_(other.release()) {}
    u_ptr& operator=(u_ptr&& other) noexcept {
        reset(other.release());
        return *this;
    }

    T& operator*() const {
        return *p_;
    }

    T* operator->() const {
        return p_;
    }

    T* get() const {
        return p_;
    }

    T* release() {
        T* ptr = p_;
        p_ = nullptr;
        return ptr;
    }
    void reset(T* ptr = nullptr) {
        delete p_;
        p_ = ptr;
    }

private:
    T* p_;
};

template<typename T>
class u_ptr<T[]>{
    public: 
    explicit u_ptr(T* ptr = nullptr) : p_(ptr) {}
    ~u_ptr() {
        delete[] p_;
    }

    // copy is prohibited
    u_ptr(const u_ptr&) = delete;
    u_ptr& operator=(const u_ptr&) = delete;

    // move is allowed
    u_ptr(u_ptr&& other) noexcept : p_(other.release()) {}
    u_ptr& operator=(u_ptr&& other) noexcept {
        reset(other.release());
        return *this;
    }

    T& operator[] (size_t index) const {
        return p_[index];
    }

    T* get() const {
        return p_;
    }

    T* release() {
        T* ptr = p_;
        p_ = nullptr;
        return ptr;
    }
    void reset(T* ptr = nullptr) {
        delete[] p_;
        p_ = ptr;
    }

private:
    T* p_;
};

int main(){
    {
        cout << "--- before move ---" << endl;
        u_ptr<Resource> p1(new Resource);
        u_ptr<Resource> p2(new Resource(7));
        cout << "p1 = " << p1.get() << endl;
        cout << "p1->data = " << p1->data << endl;
        cout << "p2 = " << p2.get() << endl;
        cout << "p2->data = " << p2->data << endl;

        p1 = std::move(p2);

        cout << "--- after move ---" << endl;
        cout << "p1 = " << p1.get() << endl;
        cout << "p1->data = " << p1->data << endl;
        cout << "p2 = " << p2.get() << endl;
        // cout << "p2->data = " << p2->data << endl;
    }
    {
        u_ptr<Resource[]> parr(new Resource[10]);
        cout << "\n Resource data = [ ";
        for(int i = 0; i < 10; ++i){
            cout << parr[i].data << " ";
        }
        cout << "]" << endl;
    }
    cout << "\nbefore quit ... " << endl;
}
```

- 输出:

```bash
--- before move ---
p1 = 0x1bc0af44970
p1->data = 0
p2 = 0x1bc0af449b0
p2->data = 7
Resource destroyed, data = 0
--- after move ---
p1 = 0x1bc0af449b0
p1->data = 7
p2 = 0
Resource destroyed, data = 7

 Resource data = [ 0 0 0 0 0 0 0 0 0 0 ]
Resource destroyed, data = 0
Resource destroyed, data = 0
Resource destroyed, data = 0
Resource destroyed, data = 0
Resource destroyed, data = 0
Resource destroyed, data = 0
Resource destroyed, data = 0
Resource destroyed, data = 0
Resource destroyed, data = 0
Resource destroyed, data = 0

before quit ...
```

- 接下来是 `share_ptr`

```cpp
#include <iostream>
#include <memory>
using namespace std;

struct Resource {
    int data;
    Resource(int d = 0) : data(d) {}
    ~Resource() {
        cout << "Resource destroyed, data = " << data << endl;
    }
};

int main(){
    {
        shared_ptr<Resource> p1(new Resource);
        cout << "p1 = " << p1.get() << endl;
        cout << "p1->data = " << p1->data << endl;
        shared_ptr<Resource> p2(p1);
        cout << "p2 = " << p2.get() << endl;
        cout << "p2->data = " << p2->data << endl;
    }
    cout << "\nbefore quit ... " << endl;
}
```

- 输出:

```bash
p1 = 0x1ee060a4970
p1->data = 0
p2 = 0x1ee060a4970
p2->data = 0
Resource destroyed, data = 0

before quit ...
```

- `share_ptr<Resource> p2(p1);` 这里用 p1 构造 p2 达成的效果是 p1 和 p2 现在管理同一份资源，这就是 `unique_ptr` 做不了的事情。

```cpp
#include <iostream>
#include <memory>
using namespace std;

struct Resource {
    int data;
    Resource(int d = 0) : data(d) {}
    ~Resource() {
        cout << "Resource destroyed, data = " << data << endl;
    }
};

int main(){
    shared_ptr<Resource> p2(new Resource(7));
    cout << "p2 = " << p2.get() << endl;
    cout << "p2->data = " << p2->data << endl;
    cout << "count: " << p2.use_count() << endl;
    {
        shared_ptr<Resource> p1(new Resource);
        cout << "p1 = " << p1.get() << endl;
        cout << "p1->data = " << p1->data << endl;
        cout << "count: " << p1.use_count() << endl;
        
        p2 = p1;

        cout << "--- after copy ---" << endl;
        cout << "p1 = " << p1.get() << endl;
        cout << "p1->data = " << p1->data << endl;
        cout << "count: " << p1.use_count() << endl;
        cout << "p2 = " << p2.get() << endl;
        cout << "p2->data = " << p2->data << endl;
        cout << "count: " << p2.use_count() << endl;
    }
    cout << "\nbefore quit ... " << endl;
    cout << "count: " << p2.use_count() << endl;
}
```

- 输出:

```bash
p2 = 0x1d85a5f4970
p2->data = 7
count: 1
p1 = 0x1d85a5f4da0
p1->data = 0
count: 1
Resource destroyed, data = 7
--- after copy ---
p1 = 0x1d85a5f4da0
p1->data = 0
count: 2
p2 = 0x1d85a5f4da0
p2->data = 0
count: 2

before quit ...
count: 1
Resource destroyed, data = 0
```

- 最后一个管理者出了生命周期时这个资源才会被释放。
- `1` 说明一个管理者在使用，降到 `0` 时资源就被回收了。
- 然后再来实现一下。
- 首先需要思考把这个 `count` 存在哪里？需要是非侵入式的设计(也就是不能在 `Resource` 里面，不能让用户自定义这个)。所以我们需要在实现 `shared_point` 的时候就把这个 `count` 实现了。

```cpp
#include <iostream>
#include <memory>
using namespace std;

struct Resource {
    int data;
    Resource(int d = 0) : data(d) {}
    ~Resource() {
        cout << "Resource destroyed, data = " << data << endl;
    }
};

template<typename T>
class s_ptr {
private:
    struct ControlBlock {
        T* p_;
        size_t ref_count;
        ControlBlock(T* ptr) : p_(ptr), ref_count(1) {}
        ~ControlBlock() {
            delete p_;
        }
    };

    ControlBlock* cb;
    void add_shared(){
        if(cb){
            cb->ref_count++;
        }
    }
    void release_shared(){
        if(cb){
            cb->ref_count--;
            if(cb->ref_count == 0){
                delete cb;
            }
        }
    }
public:
    explicit s_ptr(T* ptr = nullptr) {
        if(ptr){
            cb = new ControlBlock(ptr);
        }else{
            cb = nullptr;
        }
    }
    ~s_ptr() {
        release_shared();
    }

    s_ptr(const s_ptr& other) : cb(other.cb) {
        add_shared();
    }
    
    s_ptr& operator=(const s_ptr& other) {
        if (this != &other){
            release_shared();
            cb = other.cb;
            add_shared();
        }
        return *this;
    }

    T& operator*() const{
        return *(cb->p_);
    }

    T* operator->() const{
        return cb->p_;
    }

    // 上面两种在 cb 是 nullptr 的时候会运行出错

    T* get() const{
        return cb ? cb->p_ : nullptr;
    }

    size_t use_count() const{
        return cb ? cb->ref_count : 0;
    }
};


int main(){
    s_ptr<Resource> p2(new Resource(7));
    cout << "p2 = " << p2.get() << endl;
    cout << "p2->data = " << p2->data << endl;
    cout << "count: " << p2.use_count() << endl;
    {
        s_ptr<Resource> p1(new Resource);
        cout << "p1 = " << p1.get() << endl;
        cout << "p1->data = " << p1->data << endl;
        cout << "count: " << p1.use_count() << endl;
        
        p2 = p1;

        cout << "--- after copy ---" << endl;
        cout << "p1 = " << p1.get() << endl;
        cout << "p1->data = " << p1->data << endl;
        cout << "count: " << p1.use_count() << endl;
        cout << "p2 = " << p2.get() << endl;
        cout << "p2->data = " << p2->data << endl;
        cout << "count: " << p2.use_count() << endl;
    }
    cout << "\nbefore quit ... " << endl;
    cout << "count: " << p2.use_count() << endl;
}
```

- 输出:

```bash
p2 = 0x2a167904970
p2->data = 7
count: 1
p1 = 0x2a167904da0
p1->data = 0
count: 1
Resource destroyed, data = 7
--- after copy ---
p1 = 0x2a167904da0
p1->data = 0
count: 2
p2 = 0x2a167904da0
p2->data = 0
count: 2

before quit ...
count: 1
Resource destroyed, data = 0
```

- `s_ptr::cb` 类型是 `ControlBlock*`。每个 `s_ptr` 对象通过这个指针指向一个共享的 `ControlBlock`。如果 `s_ptr` 不管理任何对象（即为空指针），则 `cb` 为 `nullptr`。
- 整个 `main` 的运行流程。

```cpp
int main(){
    // 1. s_ptr<Resource> p2(new Resource(7));
    //    - 调用 s_ptr 构造函数。
    //    - new Resource(7) 创建一个 Resource 对象，data = 7。
    //    - new ControlBlock(Resource(7)的指针) 创建控制块 cb2。
    //      - cb2->p_ 指向 Resource(7)。
    //      - cb2->ref_count = 1。
    //    - p2.cb 指向 cb2。
    s_ptr<Resource> p2(new Resource(7));
    cout << "p2 = " << p2.get() << endl;
    cout << "p2->data = " << p2->data << endl;
    cout << "count: " << p2.use_count() << endl;

    { // 进入内部作用域
        // 2. s_ptr<Resource> p1(new Resource); (假设 Resource() 默认 data = 0)
        //    - 调用 s_ptr 构造函数。
        //    - new Resource() 创建一个 Resource 对象，data = 0。
        //    - new ControlBlock(Resource(0)的指针) 创建控制块 cb1。
        //      - cb1->p_ 指向 Resource(0)。
        //      - cb1->ref_count = 1。
        //    - p1.cb 指向 cb1。
        s_ptr<Resource> p1(new Resource);
        cout << "p1 = " << p1.get() << endl;
        cout << "p1->data = " << p1->data << endl;
        cout << "count: " << p1.use_count() << endl;

        // 3. p2 = p1; (拷贝赋值)
        //    - 调用 p2.operator=(p1)。
        //    - (this != &other) 为 true。
        //    - p2.release_shared() 被调用:
        //      - p2.cb (即 cb2) 的 ref_count 从 1 减为 0。
        //      - delete cb2; 执行。
        //        - cb2->~ControlBlock() 执行。
        //          - delete cb2->p_; (即 delete Resource(7) 指针) 执行。
        //          - 输出: "Resource destroyed, data = 7"
        //    - p2.cb = p1.cb; (现在 p2.cb 和 p1.cb 都指向 cb1)。
        //    - p2.add_shared() 被调用:
        //      - p2.cb (即 cb1) 的 ref_count 从 1 增为 2。
        p2 = p1;

        cout << "--- after copy ---" << endl;
        cout << "p1 = " << p1.get() << endl;
        cout << "p1->data = " << p1->data << endl;
        cout << "count: " << p1.use_count() << endl;
        cout << "p2 = " << p2.get() << endl;
        cout << "p2->data = " << p2->data << endl;
        cout << "count: " << p2.use_count() << endl;
    } // 内部作用域结束

    // 4. p1 析构 (~s_ptr() 被调用)
    //    - p1.release_shared() 被调用:
    //      - p1.cb (即 cb1) 的 ref_count 从 2 减为 1。
    //      - ref_count 不为 0，cb1 不会被 delete。

    cout << "\nbefore quit ... " << endl;
    cout << "count: " << p2.use_count() << endl;
} // main 函数结束

// 5. p2 析构 (~s_ptr() 被调用)
//    - p2.release_shared() 被调用:
//      - p2.cb (即 cb1) 的 ref_count 从 1 减为 0。
//      - delete cb1; 执行。
//        - cb1->~ControlBlock() 执行。
//          - delete cb1->p_; (即 delete Resource(0) 指针) 执行。
//          - 输出: "Resource destroyed, data = 0"
```

- 这里还有一个可以实现的 `swap` ，然后赋值运算可以改写。

```cpp
#include <iostream>
#include <memory>
using namespace std;

struct Resource {
    int data;
    Resource(int d = 0) : data(d) {}
    ~Resource() {
        cout << "Resource destroyed, data = " << data << endl;
    }
};

template<typename T>
class s_ptr {
private:
    struct ControlBlock {
        T* p_;
        size_t ref_count;
        ControlBlock(T* ptr) : p_(ptr), ref_count(1) {}
        ~ControlBlock() {
            delete p_;
        }
    };

    ControlBlock* cb;
    void add_shared(){
        if(cb){
            cb->ref_count++;
        }
    }
    void release_shared(){
        if(cb){
            cb->ref_count--;
            if(cb->ref_count == 0){
                delete cb;
            }
        }
    }
public:
    explicit s_ptr(T* ptr = nullptr) {
        if(ptr){
            cb = new ControlBlock(ptr);
        }else{
            cb = nullptr;
        }
    }
    ~s_ptr() {
        release_shared();
    }

    s_ptr(const s_ptr& other) : cb(other.cb) {
        add_shared();
    }
    
    s_ptr& operator=(const s_ptr& other) {
        s_ptr(other).swap(*this);
        return *this;
    }

    void swap(s_ptr& other) noexcept{
        std::swap(cb, other.cb);
    }

    T& operator*() const{
        return *(cb->p_);
    }

    T* operator->() const{
        return cb->p_;
    }

    // 上面两种在 cb 是 nullptr 的时候会运行出错

    T* get() const{
        return cb ? cb->p_ : nullptr;
    }

    size_t use_count() const{
        return cb ? cb->ref_count : 0;
    }
};


int main(){
    s_ptr<Resource> p2(new Resource(7));
    cout << "p2 = " << p2.get() << endl;
    cout << "p2->data = " << p2->data << endl;
    cout << "count: " << p2.use_count() << endl;
    {
        s_ptr<Resource> p1(new Resource);
        cout << "p1 = " << p1.get() << endl;
        cout << "p1->data = " << p1->data << endl;
        cout << "count: " << p1.use_count() << endl;
        
        p2 = p1;

        cout << "--- after copy ---" << endl;
        cout << "p1 = " << p1.get() << endl;
        cout << "p1->data = " << p1->data << endl;
        cout << "count: " << p1.use_count() << endl;
        cout << "p2 = " << p2.get() << endl;
        cout << "p2->data = " << p2->data << endl;
        cout << "count: " << p2.use_count() << endl;
    }
    cout << "\nbefore quit ... " << endl;
    cout << "count: " << p2.use_count() << endl;
}
```

- 输出:

```bash
p2 = 0x2381f5f4970
p2->data = 7
count: 1
p1 = 0x2381f5f4da0
p1->data = 0
count: 1
Resource destroyed, data = 7
--- after copy ---
p1 = 0x2381f5f4da0
p1->data = 0
count: 2
p2 = 0x2381f5f4da0
p2->data = 0
count: 2

before quit ...
count: 1
Resource destroyed, data = 0
```

- 简单来说，`this->swap(other)` 交换了两个 `s_ptr` 对象所管理的资源（即它们内部的 `ControlBlock` 指针）。
-  修改后， `s_ptr(other)` 这一部分创建了一个临时的、匿名的 `s_ptr` 对象。这个临时对象是通过调用 `s_ptr` 的拷贝构造函数 `s_ptr(const s_ptr& other)` 来创建的，其中 `other` 是赋值操作的源对象（等号右边的对象）。在拷贝构造函数中临时对象的 `cb` 会被设置为 `other.cb`。然后调用 `add_shared()`，使得 `other.cb`（现在也是临时对象的 `cb`）所指向的 `ControlBlock` 的引用计数增加 1。此时，如果 `other` 有效，临时对象已经成功地、安全地持有了对 `other` 所管理资源的一份共享所有权，并且引用计数也已正确更新。创建的临时 `s_ptr` 对象接着调用它自己的 `swap` 成员函数，参数是 `*this`（即赋值操作的目标对象，等号左边的对象）。 `*this` 对象（赋值的目标）现在持有了临时对象刚刚创建并正确管理的 `cb`（即 `other` 的资源的副本，引用计数已正确）。临时对象现在持有了 `*this` 对象**原来**的 `cb`。在整个表达式 `s_ptr(other).swap(*this);` 执行完毕后，这个临时的 `s_ptr` 对象因为生命周期结束而被销毁。临时对象的析构函数 `~s_ptr()` 会被调用。在其析构函数中，`release_shared()` 会被调用。重要的是，这个 `release_shared()` 操作的是临时对象当前持有的 `cb`——也就是 `*this` 对象**在交换之前**所持有的那个旧的 `cb`。因此，`*this` 的旧资源（如果存在）的引用计数会被正确减少，并且如果引用计数降为0，旧资源和其控制块会被正确释放。最后，按惯例返回对 `*this` 的引用，以支持链式赋值。
- 使用 `Copy-and-Swap` 的好处是强异常安全 (Strong Exception Guarantee): 这是最大的优点。赋值操作要么完全成功，要么在发生异常时对象状态回滚到操作开始前的状态（即 `*this` 保持不变）。潜在可能抛出异常的操作（主要是资源获取）都发生在临时对象的构造阶段 `s_ptr(other)`。如果这一步失败，`*this` 根本没有被修改。`swap` 操作本身是 `noexcept` 的，保证不会抛异常。临时对象的析构（释放旧资源）也是在所有关键操作成功后才发生。
- 总结 `main` 函数中 `p2 = p1;` 的流程 (使用 `Copy-and-Swap`)

1. `p2 = p1;` 开始执行。 `p2` 当前管理 `Resource(7)` (设其控制块为 `CB_7_old`，引用计数为 1)。 `p1` 当前管理 `Resource(0)` (设其控制块为 `CB_0`，引用计数为 1)。
2. `s_ptr temp(p1);` (概念上的临时对象创建)，调用拷贝构造函数 `s_ptr(p1)`。`temp.cb` 指向 `p1.cb` (即 `CB_0`)。`temp.add_shared()` 执行，`CB_0->ref_count` 从 1 变为 2。
3. `temp.swap(p2);` ， `std::swap(temp.cb, p2.cb);` ， `temp.cb` 现在指向 `p2` 原来的 `cb` (即 `CB_7_old`，其 `ref_count` 仍为 1)。`p2.cb` 现在指向 `temp` 原来的 `cb` (即 `CB_0`，其 `ref_count` 为 2)。
4. 临时对象 `temp` 销毁 (`temp.~s_ptr()`)， `temp.release_shared()` 被调用，此时 `temp.cb` 指向 `CB_7_old`。`CB_7_old->ref_count` 从 1 减为 0。`delete CB_7_old;` 执行。`CB_7_old->~ControlBlock()` 执行。`delete CB_7_old->p_;` (即 `delete Resource(7)`) 执行。输出: "Resource destroyed, data = 7"。
5. `operator=` 返回 `p2`。此时 `p2.cb` 指向 `CB_0`，`CB_0->ref_count` 为 2。`p1.cb` 仍然指向 `CB_0`，`CB_0->ref_count` 为 2。

- 然后我们尝试 `move`，先使用标准库里面的。

```cpp
#include <iostream>
#include <memory>
using namespace std;

struct Resource {
    int data;
    Resource(int d = 0) : data(d) {}
    ~Resource() {
        cout << "Resource destroyed, data = " << data << endl;
    }
};

template<typename T>
class s_ptr {
private:
    struct ControlBlock {
        T* p_;
        size_t ref_count;
        ControlBlock(T* ptr) : p_(ptr), ref_count(1) {}
        ~ControlBlock() {
            delete p_;
        }
    };

    ControlBlock* cb;
    void add_shared(){
        if(cb){
            cb->ref_count++;
        }
    }
    void release_shared(){
        if(cb){
            cb->ref_count--;
            if(cb->ref_count == 0){
                delete cb;
            }
        }
    }
public:
    explicit s_ptr(T* ptr = nullptr) {
        if(ptr){
            cb = new ControlBlock(ptr);
        }else{
            cb = nullptr;
        }
    }
    ~s_ptr() {
        release_shared();
    }

    s_ptr(const s_ptr& other) : cb(other.cb) {
        add_shared();
    }
    
    s_ptr& operator=(const s_ptr& other) {
        s_ptr(other).swap(*this);
        return *this;
    }

    void swap(s_ptr& other) noexcept{
        std::swap(cb, other.cb);
    }

    T& operator*() const{
        return *(cb->p_);
    }

    T* operator->() const{
        return cb->p_;
    }

    // 上面两种在 cb 是 nullptr 的时候会运行出错

    T* get() const{
        return cb ? cb->p_ : nullptr;
    }

    size_t use_count() const{
        return cb ? cb->ref_count : 0;
    }
};


int main(){
    shared_ptr<Resource> p2(new Resource(7));
    cout << "p2 = " << p2.get() << endl;
    cout << "p2->data = " << p2->data << endl;
    cout << "count: " << p2.use_count() << endl;
    {
        shared_ptr<Resource> p1(new Resource);
        cout << "p1 = " << p1.get() << endl;
        cout << "p1->data = " << p1->data << endl; 
        cout << "count: " << p1.use_count() << endl;
        
        p2 = std::move(p1);

        cout << "--- after move ---" << endl;
        cout << "p1 = " << p1.get() << endl;
        // cout << "p1->data = " << p1->data << endl; 这里因为移出去后变成 nullptr 了，不能再访问了。
        cout << "count: " << p1.use_count() << endl;
        cout << "p2 = " << p2.get() << endl;
        cout << "p2->data = " << p2->data << endl;
        cout << "count: " << p2.use_count() << endl;
    }
    cout << "\nbefore quit ... " << endl;
    cout << "count: " << p2.use_count() << endl;
}
```

- 输出:

```bash
p2 = 0x1e843664970
p2->data = 7
count: 1
p1 = 0x1e843664da0
p1->data = 0
count: 1
Resource destroyed, data = 7
--- after move ---
p1 = 0
count: 0
p2 = 0x1e843664da0
p2->data = 0
count: 1

before quit ...
count: 1
Resource destroyed, data = 0
```

- 接下来我们自己实现。

```cpp
#include <iostream>
#include <memory>
using namespace std;

struct Resource {
    int data;
    Resource(int d = 0) : data(d) {}
    ~Resource() {
        cout << "Resource destroyed, data = " << data << endl;
    }
};

template<typename T>
class s_ptr {
private:
    struct ControlBlock {
        T* p_;
        size_t ref_count;
        ControlBlock(T* ptr) : p_(ptr), ref_count(1) {}
        ~ControlBlock() {
            delete p_;
        }
    };

    ControlBlock* cb;
    void add_shared(){
        if(cb){
            cb->ref_count++;
        }
    }
    void release_shared(){
        if(cb){
            cb->ref_count--;
            if(cb->ref_count == 0){
                delete cb;
            }
        }
    }
public:
    explicit s_ptr(T* ptr = nullptr) {
        if(ptr){
            cb = new ControlBlock(ptr);
        }else{
            cb = nullptr;
        }
    }
    ~s_ptr() {
        release_shared();
    }

    s_ptr(const s_ptr& other) : cb(other.cb) {
        add_shared();
    }
    
    s_ptr& operator=(const s_ptr& other) {
        s_ptr(other).swap(*this);
        return *this;
    }

    void swap(s_ptr& other) noexcept{
        std::swap(cb, other.cb);
    }

    s_ptr(s_ptr &&other) noexcept : cb(other.cb){
        other.cb = nullptr;
    }

    s_ptr& operator=(s_ptr&& other) noexcept{
        s_ptr(std::move(other)).swap(*this);
        return *this;
    }

    T& operator*() const{
        return *(cb->p_);
    }

    T* operator->() const{
        return cb->p_;
    }

    // 上面两种在 cb 是 nullptr 的时候会运行出错

    T* get() const{
        return cb ? cb->p_ : nullptr;
    }

    size_t use_count() const{
        return cb ? cb->ref_count : 0;
    }
};


int main(){
    s_ptr<Resource> p2(new Resource(7));
    cout << "p2 = " << p2.get() << endl;
    cout << "p2->data = " << p2->data << endl;
    cout << "count: " << p2.use_count() << endl;
    {
        s_ptr<Resource> p1(new Resource);
        cout << "p1 = " << p1.get() << endl;
        cout << "p1->data = " << p1->data << endl; 
        cout << "count: " << p1.use_count() << endl;
        
        p2 = std::move(p1);

        cout << "--- after move ---" << endl;
        cout << "p1 = " << p1.get() << endl;
        // cout << "p1->data = " << p1->data << endl; 这里因为移出去后变成 nullptr 了，不能再访问了。
        cout << "count: " << p1.use_count() << endl;
        cout << "p2 = " << p2.get() << endl;
        cout << "p2->data = " << p2->data << endl;
        cout << "count: " << p2.use_count() << endl;
    }
    cout << "\nbefore quit ... " << endl;
    cout << "count: " << p2.use_count() << endl;
}
```

- 输出:

```bash
p2 = 0x260c30f4970
p2->data = 7
count: 1
p1 = 0x260c30f4da0
p1->data = 0
count: 1
Resource destroyed, data = 7
--- after move ---
p1 = 0
count: 0
p2 = 0x260c30f4da0
p2->data = 0
count: 1

before quit ...
count: 1
Resource destroyed, data = 0
```

- 一般还有一个 `reset` 的功能也可以用上 `swap`。

```cpp
#include <iostream>
#include <memory>
using namespace std;

struct Resource {
    int data;
    Resource(int d = 0) : data(d) {}
    ~Resource() {
        cout << "Resource destroyed, data = " << data << endl;
    }
};

template<typename T>
class s_ptr {
private:
    struct ControlBlock {
        T* p_;
        size_t ref_count;
        ControlBlock(T* ptr) : p_(ptr), ref_count(1) {}
        ~ControlBlock() {
            delete p_;
        }
    };

    ControlBlock* cb;
    void add_shared(){
        if(cb){
            cb->ref_count++;
        }
    }
    void release_shared(){
        if(cb){
            cb->ref_count--;
            if(cb->ref_count == 0){
                delete cb;
            }
        }
    }
public:
    explicit s_ptr(T* ptr = nullptr) {
        if(ptr){
            cb = new ControlBlock(ptr);
        }else{
            cb = nullptr;
        }
    }
    ~s_ptr() {
        release_shared();
    }

    s_ptr(const s_ptr& other) : cb(other.cb) {
        add_shared();
    }
    
    s_ptr& operator=(const s_ptr& other) {
        s_ptr(other).swap(*this);
        return *this;
    }

    void swap(s_ptr& other) noexcept{
        std::swap(cb, other.cb);
    }

    s_ptr(s_ptr &&other) noexcept : cb(other.cb){
        other.cb = nullptr;
    }

    s_ptr& operator=(s_ptr&& other) noexcept{
        s_ptr(std::move(other)).swap(*this);
        return *this;
    }

    void reset(T* ptr = nullptr){
        s_ptr(ptr).swap(*this);
    }

    T& operator*() const{
        return *(cb->p_);
    }

    T* operator->() const{
        return cb->p_;
    }

    // 上面两种在 cb 是 nullptr 的时候会运行出错

    T* get() const{
        return cb ? cb->p_ : nullptr;
    }

    size_t use_count() const{
        return cb ? cb->ref_count : 0;
    }
};


int main(){
    s_ptr<Resource> p2(new Resource(7));
    cout << "p2 = " << p2.get() << endl;
    cout << "p2->data = " << p2->data << endl;
    cout << "count: " << p2.use_count() << endl;
    {
        s_ptr<Resource> p1(new Resource);
        cout << "p1 = " << p1.get() << endl;
        cout << "p1->data = " << p1->data << endl; 
        cout << "count: " << p1.use_count() << endl;
        
        p2 = std::move(p1);

        cout << "--- after move ---" << endl;
        cout << "p1 = " << p1.get() << endl;
        // cout << "p1->data = " << p1->data << endl; 这里因为移出去后变成 nullptr 了，不能再访问了。
        cout << "count: " << p1.use_count() << endl;
        cout << "p2 = " << p2.get() << endl;
        cout << "p2->data = " << p2->data << endl;
        cout << "count: " << p2.use_count() << endl;
    }
    cout << "\nbefore quit ... " << endl;
    cout << "count: " << p2.use_count() << endl;
}
```

- 输出:

```bash
p2 = 0x241764c4970
p2->data = 7
count: 1
p1 = 0x241764c4da0
p1->data = 0
count: 1
Resource destroyed, data = 7
--- after move ---
p1 = 0
count: 0
p2 = 0x241764c4da0
p2->data = 0
count: 1

before quit ...
count: 1
Resource destroyed, data = 0
```

---

## Further reading

<div class="card file-block" markdown="1">
<div class="file-icon"><img src="/Notebook/assets/images/pdf.svg" style="height: 3em;"></div>
<div class="file-body">
<div class="file-title"> Effective_Modern_C++__Item-18 </div>
<div class="file-meta"> 567 KB / 2025-05-25</div>
</div>
<a class="down-button" target="_blank" href="/Notebook/Computer_Science/OOP/[Further Readings] Effective_Modern_C++__Item-18.pdf" markdown="1">:fontawesome-solid-download: 下载</a>
</div>

---