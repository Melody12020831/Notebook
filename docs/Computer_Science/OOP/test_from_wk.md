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