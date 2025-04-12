---
statistics: True
comments: true
---

# WK's 课前小测

!!! abstract
    wk 老师班似乎是有课前测试的，我在智云上扒下来，整理记录一下，便于期末复习吧。

## W2 课前小测

???+ question
    Given two string variables strA = "apple" and strB = "banana", which of the following operations will result in a string "applebanana"?

    A. `strA - strB;`

    B. `strA * strB;`

    C. `strA + strB;`

    D. `strA / strB;`

??? note "answer"
    ```cpp
    strA + strB
    ```

---

???+ question
    If you have a string variable s* "programming" and you want to change the first character to 'P', which code snippet should you use?

    A. `s[1] = 'P';`

    B. `s(0) = 'P';`

    C. `s[0] = 'P';`

    D. `s{0} = 'P';`


??? note "answer"
    ```cpp
    s[0] = 'P';
    ```

    或者可以使用

    ```cpp
    s.at(0) = 'P';
    ```

---

???+ question
    You have a string variable str = "hello" and a pointer ps to this string. How do you call the length() function using the pointer?

    A. `*ps.length();`

    B. `ps.length();`

    C. `ps->length();`

    D. `&ps.length();`

??? note "answer"
    ```cpp
    ps->length();
    ```

    `ps` 是一个指向 `std::string` 对象的指针，通过指针访问对象的成员函数时，需要使用 `->` 操作符。

    A. `*ps.length()` 的优先级会导致 `ps.length()` 先被计算，而 `ps` 是指针类型，没有 `length()` 成员函数。如果 `ps` 是 `std::string*` 类型，`ps.length()` 本身就会报错。

    B. `ps` 是指针类型，不能直接使用 `.` 操作符调用成员函数。

    D. `&ps.length()` 试图获取 `length()` 函数的地址，而不是调用它。

---

???+ question
    Suppose you have two string variables strX and strY, and you want to assign the value of strY to strX. Which statement is correct?

    A. `strX == strY;`

    B. `strX = strY;`

    C. `strX & strY;`

    D. `strX + strY;`

??? note "answer"
    ```cpp
    strX = strY;
    ```

---

???+ question
    If you want to read a whole line of input into a string variable named line, which code should you use?

    A. `cin >> line;`

    B. `cout << line;`

    C. `getline(cin, line);`

    D. `line = cin;`

??? note "answer"
    ```cpp
    std::getline(std::cin, line);
    ```

---

## W3 课前小测

???+ question
    You have a list of integers 'lst' and you want to remove all elements that are divisibleby 3. Which of the following code snippets would achieve this?

    A. `for (auto it = lst.begin(); it!= lst.end(); ++it){ if (*it % 3 == 0) lst.erase(it);}`

    B. `auto it = lst.begin(); while (it!= lst.end()){ if (*it % 3 == 0)it = lst.erase(it); else ++it; }`
    
    C. `for (inti=0;i< lst.size();i++){ if (lst[i] % 3 == 0)Ist.erase(i);}`

??? note "answer"
    B. `auto it = lst.begin(); while (it!= lst.end()){ if (*it % 3 == 0)it = lst.erase(it); else ++it; }`

---

???+ question
    You have a map 'm' of type `map<string, int>` and you want to check if the key 'apple' exists in the map. If it does, you want to print its value; otherwise, you want to print 'Not found' Which of the following code snippets would you use?

    A. `if (m['apple"]!= 0) cout << m['apple']; else cout << 'Not found';`

    B. `if (m.count('apple')) cout << m['apple']; else cout <<'Not found';`

    C. `if (m.find('apple') == m.end()) cout << m['apple']; else cout << 'Not found';`

??? note "answer"
    B. `if (m.count('apple')) cout << m['apple']; else cout <<'Not found';`

    A 这个选项的问题在于，`m['apple']` 会直接访问键 `'apple'`，如果键不存在，`std::map` 会自动插入一个默认构造的值（对于 `int` 类型，默认值是 `0`）。因此，即使键 `'apple'` 不存在，`m['apple']` 也会返回 `0`，这会导致逻辑错误，无法正确判断键是否存在。

    C 这个选项的逻辑是错误的。`m.find('apple')` 返回一个迭代器，如果键存在，迭代器指向该键值对；如果键不存在，迭代器等于 `m.end()`。因此，正确的逻辑应该是 `if (m.find('apple') != m.end())`，表示键存在。当前代码的逻辑是反的，会导致错误的结果。

---

???+ question
    You have a vector 'v' of integers and you want to print all elements in reverse order.
    
    Which of the following code snippets would you use?
    
    A. `for (int i= 0; i< v.size(); i++) cout << v[v.size()-i-1] << '';`
    
    B. `for (auto it = v.begin(); it!= v.end(); ++it) cout << *it <<'';`
    
    C. `for (int i = v.size(); i > 0; i--) cout << v[i] <<'';`

    D. `for (auto it = v.end(); it!= v.begin(); --it) cout << *it <<'';`

??? note "answer"
    A. `for (int i= 0; i< v.size(); i++) cout << v[v.size()-i-1] << '';`

    B. 这个选项是错误的。它使用正向迭代器 `it`，从 `v.begin()` 开始遍历到 `v.end()`，打印的是元素的原始顺序，而不是逆序。

    C. 这个选项是错误的。`i` 的初始值是 `v.size()`，而 `vector` 的索引是从 `0` 到 `v.size() - 1`。直接使用 `v[i]` 会导致越界访问（访问 `v[v.size()]` 是未定义行为）。此外，循环条件应为 `i >= 0`，否则会跳过第一个元素。

    D. 这个选项是错误的。`v.end()` 指向的是容器末尾的下一个位置，而不是最后一个元素。直接解引用 `v.end()` 会导致未定义行为。此外，循环条件 `it != v.begin()` 会导致跳过第一个元素。即使修正为 `it != v.begin() - 1`，也需要小心处理迭代器的边界。

---

???+ question
    You have a list 'L' of strings and you want to insert a new string 'new_str' in alphabetical order. Which of the following code snippets would you use?

    A. `auto it = L.begin(); while (it!= L.end()&& *it < 'new_str') ++it; L.insert(it, 'new_str');`
    
    B. `auto it = L.end(); while (it!= L.begin()&& *it>'new_str')--it; L.insert(it, 'new_str');`

    C.  `for (auto it = L.begin(); it!= L.end();++it){if (*it > 'new_str') L.insert(it, 'new_str'); break;}`
    
    D. L.push_back('new_str'); L.sort();

??? note "answer"
    A. `auto it = L.begin(); while (it!= L.end()&& *it < 'new_str') ++it; L.insert(it, 'new_str');`

    B. 这个选项是错误的。`it` 从 `L.end()` 开始，但 `L.end()` 指向的是容器末尾的下一个位置，不能直接解引用 `*it`。此外，即使修正为 `--it` 后再解引用，逻辑也不如选项 A 直观和高效。

    C. 这个选项是错误的。`break` 语句会导致循环在第一次满足 `*it > 'new str'` 时立即退出，即使后面还有更小的元素需要检查。

    D. 这个选项虽然可以实现目标，但效率较低。`push_back` 将 `'new_str'` 添加到列表末尾，然后调用 `sort` 对整个列表重新排序。这种方法的时间复杂度是 &O(N \log N)$，而直接找到插入位置并插入的时间复杂度是 $O(N)$。因此，这种方法不推荐。

!!! info
    看到 `end()` 时就要时刻谨慎，要 `end() - 1`。

---

## W4 课前小测

???+ question
    在C++中，标准头文件结构为什么要使用 #ifndef、#define 和 #endif?
    
    A. 为了提高头文件的编译速度
    
    B. 为了防止头文件被重复包含，避免编译错误
    
    C. 为了让头文件的内容更加清晰易读
    
    D. 为了在头文件中定义全局变量

??? note "answer"
    B. 为了防止头文件被重复包含，避免编译错误

    #ifndef 和 #endif 是预处理指令，用于防止头文件被重复包含。当编译器第一次遇到头文件时，它会检查是否已经定义了某个特定的宏。如果没有定义，那么编译器会定义这个宏，并继续编译头文件的内容。如果已经定义了，那么编译器会忽略头文件的内容，从而避免了重复包含的问题。

    这种方法可以确保头文件的内容只被编译一次，从而提高了编译速度并避免了编译错误。

---

???+ question
    为什么在C++中，类的声明和成员函数的原型要放在头文件中，而成员函数的定义要放在源文件中?

    A. 为了让编译器能同时处理多个文件，提高编译效率

    B. 因为头文件只能包含声明，源文件只能包含定义

    C. 这样做可以将接口(头文件)和实现(源文件)分离,便于代码的维护和复用

    D. 为了让代码看起来更整齐

??? note "answer"
    C. 这样做可以将接口(头文件)和实现(源文件)分离,便于代码的维护和复用

---

???+ question
    构造函数的作用是什么?

    A. 构造函数用于在对象销毁时进行清理工作

    B. 构造函数用于创建对象时自动进行初始化，确保对象在使用前具有正确的初始值

    C. 构造函数用于定义对象的类型

    D. 构造函数用于调用其他成员函数

??? note "answer"
    B. 构造函数用于创建对象时自动进行初始化，确保对象在使用前具有正确的初始值

---

???+ question
    为什么成员函数中可以使用 this 指针?

    A. this指针是一个全局变量，可以在任何地方使用

    B. this指针是成员函数的隐藏参数，指向调用该函数的对象，在成员函数内部可以直接使用
    
    C. this指针是编译器自动创建的，用于区分不同的对象

    D. this指针是为了在成员函数中调用其他成员函数而存在的

??? note "answer"
    B. this指针是成员函数的隐藏参数，指向调用该函数的对象，在成员函数内部可以直接使用

    this指针是C++中的一种特殊指针，用于指向当前对象的地址。在成员函数中，可以使用this指针来访问当前对象的成员变量和成员函数。this指针是隐含的，不需要显式地声明，可以直接在成员函数中使用。

---

???+ question
    默认构造函数的特点是什么?

    A. 默认构造函数不能有参数
    
    B. 默认构造函数是在类没有任何构造函数时，由编译器自动创建的

    C. 默认构造函数是可以在没有参数的情况下被调用的构造函数

    D. 默认构造函数的名称与类名不同

??? note "answer"
    C. 默认构造函数是可以在没有参数的情况下被调用的构造函数

    默认构造函数不是编译器自动给的构造函数。
    
    默认构造函数的定义是参数表为空的构造函数。
    
    自己写的参数表为空的构造函数是默认构造函数。
    
    没有构造函数，编译器给的叫做自动默认构造函数，是什么都不干的。

---

## W5 课前小测

???+ question
    What does the 'private' keyword mean in the context of class members?
    
    A. All member declarations that follow are available to everyone.

    B. No one can access that member except inside function members of that type.

    C. It explicitly grants access to a function that isn't a member of the structure.

    D. It means the member has a global scope and can be accessed from anywhere.

??? note "answer"
    B. No one can access that member except inside function members of that type.

    在类的成员上下文中，`private` 关键字的作用是限制成员的访问权限。

    选项A错误，因为 `private` 的作用是限制而非开放访问权限（开放权限对应的是 `public`）。

    选项B正确，`private` 成员只能被同一类内部的成员函数访问，外部代码或其他类无法直接访问。

    选项C错误，`private` 本身不主动授予权限；若需允许外部访问，需通过友元（`friend`）机制显式声明，但这与 `private` 的关键字功能无关。

    选项D错误，`private` 成员的作用域仅限于类内部，而非全局。

---

???+ question
    What is the difference between a 'class' and a 'struct' in terms of access control?

    A. A class defaults to public, while a struct defaults to private.

    B. Both class and struct default to public.

    C. A class defaults to private, while a struct defaults to public.

    D. Both class and struct default to private.

??? note "answer"
    C. A class defaults to private, while a struct defaults to public.

    在C++中，`class` 和 `struct` 在访问控制上的核心区别是：

    - `class` 的默认成员访问权限是 `private`（私有）。

    - `struct` 的默认成员访问权限是 `public`（公开）。

    除访问权限外，二者的默认继承方式也不同：

    `class` 默认 `private` 继承。

    `struct` 默认 `public` 继承。

??? note "about private and public inheritance"
    ```cpp
    #include <iostream>
    using namespace std;

    // 基类
    class Base {
    public:
        void publicMethod()   { cout << "Base::publicMethod" << endl; }
    protected:
        void protectedMethod() { cout << "Base::protectedMethod" << endl; }
    private:
        void privateMethod()  { cout << "Base::privateMethod" << endl; }
    };

    // 默认继承方式：class 使用 private 继承
    class DerivedClass : Base {  // 等价于 class DerivedClass : private Base
    public:
        void test() {
            publicMethod();     // 可访问：Base的public成员在DerivedClass中变为private
            protectedMethod();  // 可访问：Base的protected成员在DerivedClass中变为private
            // privateMethod(); // 错误：Base的private成员始终不可访问
        }
    };

    // 默认继承方式：struct 使用 public 继承
    struct DerivedStruct : Base {  // 等价于 struct DerivedStruct : public Base
        void test() {
            publicMethod();     // 可访问：Base的public成员保持public
            protectedMethod();  // 可访问：Base的protected成员保持protected
            // privateMethod(); // 错误：Base的private成员不可访问
        }
    };

    int main() {
        DerivedClass dc;
        // dc.publicMethod();   // 错误：DerivedClass中publicMethod是private（因private继承）
        dc.test();              // 正确：通过派生类的public方法间接访问基类成员

        DerivedStruct ds;
        ds.publicMethod();      // 正确：DerivedStruct中publicMethod保持public（因public继承）
        ds.test();

        return 0;
    }
    ```

    建议显式写出继承方式（如 `class Derived : public Base`），避免依赖默认行为导致歧义。

---

???+ question
    What is the lifetime of a local variable?

    A. It persists only for the period that a constructor or method executes.
    
    B. It lasts as long as the object lasts.
    
    C. It has a global lifetime, starting before main() andending after main() exits.
    
    D. It is constructed once and destroyed on exit from the program.

??? note "answer"
    A. It persists only for the period that a constructor or method executes.

    选项A正确。局部变量的生命周期仅限于其所在的代码块（如函数、构造函数、方法或 {} 包围的作用域）执行期间。当代码块执行完毕（或离开作用域时），局部变量会被自动销毁。

    选项B错误。局部变量与对象生命周期无关，它仅存在于代码块执行过程中，而非对象存在的整个周期。

    选项C错误。全局生命周期属于全局变量或静态变量，而非局部变量。

    选项D错误。局部变量在每次进入作用域时构造，离开时销毁，而非程序退出时才销毁（静态局部变量例外，但题目未特指）。

---

???+ question
    What does a static member function mean in C++?
    
    A. It has an implicit receiver(this) and can access member variables.
    
    B. It is shared by instances,can only access static member variables, and has no implicit receiver(this).
    
    C. It is a function with internal linkage and can be dynamically overridden.
    
    D. It is a function that is called only once during the program execution.

??? note "answer"
    B. It is shared by instances,can only access static member variables, and has no implicit receiver(this).

    在C++中，静态成员函数（static member function） 的核心特性如下：

    1. 属于类本身，而非类的实例：静态成员函数与类的实例无关，可直接通过类名调用（无需创建对象）。

    2. 无隐式 this 指针：静态成员函数没有隐式传递的 this 指针，因此 无法直接访问类的非静态成员变量或非静态成员函数。

    3. 只能访问静态成员：静态成员函数仅能访问类的静态成员变量和其他静态成员函数（因为静态成员属于类，而非特定实例）。

    4. 共享性：所有类的实例共享同一个静态成员函数。

    C. 错误。静态成员函数的链接属性与普通函数类似（默认外部链接），且不能是虚函数（无法动态覆盖）。

    D. 错误。静态成员函数可被多次调用，其调用次数不受限制。

---

???+ question
    When is the constructor of a global object called?
    
    A. When the object is first accessed in the program.
    
    B. Before main() is entered.

    C. At the end of the program execution.
    
    D. When the function containing the object definition is called.

??? note "answer"
    B. Before main() is entered.

    选项A错误。全局对象的构造函数与是否被访问无关。即使从未被使用，构造函数仍会在程序启动时调用（不同于局部静态变量首次访问时才初始化）。

    选项B正确。全局对象的构造函数在程序启动阶段、main() 函数执行之前完成初始化。这是为了确保全局对象在程序逻辑开始前已就绪。

    选项C错误。C描述的是析构函数的调用时机，而非构造函数。全局对象的析构函数在 main() 结束后、程序退出前调用。

    选项D错误。D描述的是局部对象的构造函数调用时机（如函数内定义的变量），与全局对象无关。

---

## W6 课前小测

???+ question
    What is the main difference between a reference and a pointer in C++?

    A. References can be null, while pointers cannot.

    B. References are independent of existing variables, while pointers are aliases for variables.
    
    C. References can't change to a new "address" location, while pointers can.
    
    D. References can change to point to a different address, while pointers cannot.

??? note "answer"
    C. References can't change to a new "address" location, while pointers can.

    在 C++ 中，**引用（Reference）** 和 **指针（Pointer）** 的主要区别在于它们的初始化、可变性和空值特性：

    | **特性**            | **引用**                                     | **指针**                                   |
    |:-------------------:|:-------------------------------------------:|:-----------------------------------------:|
    | **初始化**          | 必须初始化（绑定到一个对象），不能为 `null` | 可以不初始化（但应避免野指针）或设为 `nullptr` |
    | **可变性**          | 一旦绑定后，不可重新绑定到其他对象         | 可以随时指向不同的地址（重新赋值）         |
    | **内存占用**        | 无独立内存地址（是对象的别名）             | 有独立内存地址（存储指向的地址值）         |
    | **语法操作**        | 直接访问对象（无需解引用）                 | 需要解引用（`*ptr`）才能访问对象          |

---

???+ question
    Which of the following statements about right-value references is correct?
    
    A. A right-value reference can be initialized by a left-value. 
    
    B. Once a right-value reference is initialized, it remains a right-value.
    
    C. A right-value reference can extend the lifetime of a right value.
    
    D. A right-value reference can be declared without initialization.

??? note "answer"
    C. A right-value reference can extend the lifetime of a right value.
    
    A. 错误。右值引用不能直接由左值初始化。右值引用(&&)只能绑定到右值。如果要将左值转换为右值引用，需要使用std::move()函数。
    
    B. 错误。一旦右值引用被初始化，它实际上变成了一个左值，因为它有名字且可以取地址。这就是所谓的"引用折叠"现象。
    
    C. 正确。这是右值引用的一个重要特性。通过将临时对象(右值)绑定到右值引用，可以延长该临时对象的生命周期，使其持续到引用的作用域结束。
    
    D. 错误。右值引用必须在声明时初始化，就像普通引用一样。不能声明一个未初始化的引用。

---

???+ question
    What is the purpose of using const in C++?
    
    A. To make a variable mutable.
    
    B. To declare a variable with a constant value that cannot be changed.
    
    C. To allow a variable to be assigned a new value at anytime.
    
    D. To make a variable have external linkage by default.

??? note "answer"
    B. To declare a variable with a constant value that cannot be changed.

    A. 错误。const的作用恰恰相反，它使变量不可变(immutable)而不是可变(mutable)。C++中有mutable关键字，其作用是允许在const成员函数中修改被标记为mutable的成员变量。

    B. 正确。const的主要目的就是声明一个不能被修改的常量。一旦初始化后，const变量的值就不能再被改变。

    C. 错误。这与const的目的完全相反。const防止变量在初始化后被重新赋值。
    
    D. 错误。在C++中，const变量默认具有内部链接(internal linkage)，而不是外部链接(external linkage)。这与C语言中的行为不同。在C++中，如果需要使const变量具有外部链接，需要显式使用extern关键字。


---

???+ question
    What is the role of a const member function in a class?
    
    A. It can modify the object's data members.
    
    B. It can call non-const member functions
    
    C. It cannot modify the object's data members and is safe for const objects.
    
    D. It can only be called by non-const objects.

??? note "answer"
    C. It cannot modify the object's data members and is safe for const objects.
    
    A. 错误。const成员函数的主要特点就是它不能修改对象的数据成员（除非这些成员被声明为mutable）。这是const成员函数的基本限制。
    
    B. 错误。const成员函数不能调用非const成员函数，因为非const成员函数可能会修改对象状态，这违反了const成员函数的承诺。
    
    C. 正确。const成员函数不能修改调用它的对象的数据成员，这保证了对象的状态不变。因此，const对象只能调用const成员函数，因为非const成员函数可能会尝试修改对象。
    
    D. 错误。const成员函数可以被const对象和非const对象调用。事实上，const成员函数的一个主要用途就是允许const对象调用类的方法。

---

## W7 课前小测

???+ question
    What is the main purpose of using delegating constructors?
    
    A. To reduce code duplication in overloaded constructors

    B. To increase the number of constructors in a class
    
    C. To make the constructor calls more complex
    
    D. To avoid using initialization lists

??? note "answer"
    The main purpose of using delegating constructors is **A. To reduce code duplication in overloaded constructors**.

    委托构造函数的主要目的是 **A. 减少重载构造函数中的代码重复**。

    在一个类中，我们经常会定义多个构造函数（重载构造函数），它们可能接受不同数量或类型的参数来初始化对象的不同部分。然而，这些不同的构造函数通常会包含一些共同的初始化逻辑。

    使用委托构造函数允许一个构造函数调用同一个类中的另一个构造函数来执行这部分共同的初始化代码。这样一来，只需要在一个“主”构造函数中编写这些共同的初始化逻辑，其他的构造函数只需要委托给这个“主”构造函数即可，从而避免了在每个构造函数中都编写相同的代码，**显著减少了代码的冗余，提高了代码的可维护性和可读性**。

    **B.** 委托构造函数本身并不会直接增加类中构造函数的数量。它的目的是为了更好地组织和管理已有的构造函数。

    **C.** 委托构造函数实际上是为了简化构造函数的逻辑，而不是使其更复杂。通过将共同的初始化逻辑集中在一个地方，可以使每个单独的构造函数调用更加清晰和简洁。

    **D.** 委托构造函数和初始化列表是不同的概念，它们可以一起使用。初始化列表用于直接初始化成员变量，而委托构造函数用于调用另一个构造函数。委托的构造函数内部仍然可以使用初始化列表。

---

???+ question
    What is a key property of default arguments?

    A. They are defined in the function head
    
    B. They are declared in the prototype and the compiler inserts them if no value is provided in the function call
    
    C. They can be added from left to right in the argument list
    
    D. They cannot be used in constructors

??? note "answer"
    - 首先要注意的是，argument 是函数调用时传过去的值，而 parameter 是函数接收值的那个参数。

    The key property of default arguments is **B. They are declared in the prototype and the compiler inserts them if no value is provided in the function call**.

    **A.** 当你定义一个函数时，你可以在参数列表中为某些参数指定一个默认值。如果在调用该函数时没有为这些参数提供实际的值，那么函数将使用在函数定义中指定的默认值。首先这里是声明而不是定义，所以 `define` 是错的。其次 `function head` 既可以用来指 `propertype` 也可以用来指函数定义时的函数的头部，所以不是一个准确的答案。

    **B.** 在某些语言（如 C++）中，函数原型可以包含默认参数。编译器在编译时会处理默认参数的缺失情况，但默认值本身是在函数定义时确定的。

    **C.** 这是**错误**的。默认参数有一个重要的限制：**一旦你在参数列表中为一个参数提供了默认值，那么它右边的所有参数都必须也提供默认值**。你不能在没有默认值的参数后面定义有默认值的参数。

    **D.** 这是**错误**的。默认参数**可以**在类的构造函数中使用，这为创建对象提供了更灵活的方式。例如，你可以定义一个构造函数，某些参数有默认值，这样在创建对象时可以只提供必要的部分信息。


---

???+ question
    What is the main advantage of using inline functions?

    A. They always reduce the code size

    B. They eliminate the overhead of function calls
    
    C. They can be used for recursive functions
    
    D. They don't need to be declared in the header file

??? note "answer"
    The main advantage of using inline functions is **B. They eliminate the overhead of function calls**.

    使用内联函数的主要优点是 **B. 它们消除了函数调用的开销**。

    **B.** 这是内联函数最核心的优势。当编译器遇到对内联函数的调用时，它不会像普通函数那样生成函数调用的指令（例如，将参数压入堆栈、跳转到函数地址、执行函数体、返回等）。相反，编译器会将内联函数的代码**直接插入**到调用该函数的地方，就像那部分代码本来就在那里一样。这样就避免了函数调用时的时间和空间开销，从而提高了程序的执行效率，尤其对于频繁调用的小型函数来说效果更明显。

    **A.** 这是**错误**的。虽然内联展开可以提高执行效率，但如果一个内联函数在多个地方被调用，那么它的代码会被复制多次，这可能会导致最终的可执行文件**增大**。因此，内联函数并不总是能减小代码大小，有时反而会增大。

    **C.** 这是**错误**的。理论上可以将递归函数声明为内联的，但编译器通常会**忽略**对递归函数的内联请求。因为递归的本质是函数自身的重复调用，如果每次调用都进行内联展开，可能会导致代码无限膨胀，而且也无法真正消除函数调用的开销。

    **D.** 这是**错误**的。为了让编译器在调用内联函数的地方能够进行内联展开，编译器需要知道内联函数的定义。因此，通常**内联函数的定义（包括函数体）需要放在头文件中**，以便在包含该头文件的所有源文件中都可见。


---

???+ question
    What is the key difference between a delegating constructor and a targetconstructor?
    
    A. A delegating constructor can have other members initialized in its own initialization list, while a target constructor cannot
    
    B. The execution of the target constructor precedes that of the delegating constructor
    
    C. A target constructor can delegate to another constructor, while a delegating constructor cannot

    D. A delegating constructor is always private, while a targetconstructor is always public

??? note "answer"
    The key difference between a delegating constructor and a target constructor is **B. The execution of the target constructor precedes that of the delegating constructor**.

    委托构造函数 (delegating constructor) 和目标构造函数 (target constructor) 之间的关键区别在于 **B. 目标构造函数的执行先于委托构造函数**。

    - **委托构造函数 (Delegating Constructor):** 这是一个构造函数，它的主要任务是**调用同一个类中的另一个构造函数**来完成部分或全部的初始化工作。它将自身的初始化职责委托给了另一个构造函数。

    - **目标构造函数 (Target Constructor):** 这是**被委托构造函数调用的那个构造函数**。它包含了实际执行初始化逻辑的代码。

    因此，当一个委托构造函数被调用时，它的执行流程是这样的：

    1.  委托构造函数首先在其初始化列表中**调用目标构造函数**。
    2.  **目标构造函数首先执行其全部的代码**，完成一部分或全部的成员变量初始化。
    3.  **只有在目标构造函数执行完毕后**，委托构造函数才会继续执行其自身的代码（如果有的话，通常其函数体为空或只包含一些额外的、在目标构造函数之后才需要执行的逻辑）。

    **A.** 这是**错误**的。无论是委托构造函数还是目标构造函数，都可以在其自身的初始化列表中初始化成员变量。委托构造函数除了可以调用另一个构造函数外，也可以同时初始化一些自身的成员。

    **C.** 这是**错误**的。委托关系是单向的。一个构造函数可以委托给另一个构造函数，成为委托构造函数。被委托的构造函数（目标构造函数）不能再委托给其他的构造函数，以避免无限循环的委托调用。

    **D.** 这是**错误**的。委托构造函数和目标构造函数的访问修饰符（public, private, protected）取决于类的设计需求，并没有强制的规定。一个公有的构造函数可以委托给另一个公有的或私有的构造函数。

---