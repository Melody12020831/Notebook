---
statistics: True
comments: true
---

!!! abstract
    wk 老师班似乎是有课前测试的，我在智云上扒下来，整理记录一下，便于期末复习吧。

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


