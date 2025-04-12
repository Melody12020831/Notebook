---
statistics: True
comments: true
---

# Chapter 3 | STL

STL = Standard Template Library

- Part of the ISO Standard C++ Library
- Data Structures and algorithms for C++

**Why should I use STL?**

- Reduced development time
    - Utilities well designed and written.
- Code Readability
    - More meaningful stuff filled in one page.
- Robustness
    - Thoroughly used and tested.
- Portable code
- Maintainable code

---

## Three parts of STL

- Containers
    - class templates, common data structures.
- Algorithms
    - Functions that operate on ranges of elements.
- Iterators
    - Generalization of pointers, access elements in a uniform manner.

---

### Containers

**A personal notebook**

- It allows notes to be stored.
- It has no limit on the number of notes it can store.
- It will show individual notes.
- It will tell us how many notes it is currently storing.
- Array can not be used here.

#### Sequential

- `array` (static) as "array"
- `vector` (dynamic) variable array
- `deque` (double-ended queue) dual-end queue
- `forward_list` (singly-linked) as it
- `list` (doubly-linked) double-linked-list
- `string` char.array

##### `vector`

- Constructor / Destructor
- Element access
    - `at` , `operator[]` , `front` , `back` , `data`
- Iterators
    - `begin` , `end` , `cbegin` , `cend`
- Capacity
    - `empty` , `size` , `reserve` , `capacity`
- Modifiers
    - `clear` , `insert` , `erase` , `push_back`

---

**From cppreference:**

`vector` 的存储是自动管理的，按需扩张收缩。

`vector` 所用的方式不在每次插入元素时，而只在额外内存耗尽时进行重分配。分配的内存总量可用 `capacity()` 函数查询。

- Element access

```cpp
std::vector<int> data{1, 2, 4, 5, 5, 6};
data.at(1) = 88;
data[0] = 5;
data.front() = 10;  // data.front() 等价于 *data.begin()
data.back() = 20;  // data.back() 等价于 *std::prev(data.end())

pointer_func(data.data(), data.size());
// 返回指向作为元素存储工作的底层数组的指针。
// 返回的指针使得范围 [data(), data() + size()) 始终是有效范围，即使容器为空（此时 data() 不可解引用）。
```

- Iterators

1. `begin` 返回指向 `vector` 首元素的迭代器。如果 `vector` 为空，那么返回的迭代器等于 `end()`。

`begin` 返回普通迭代器或 `const` 迭代器，具体取决于容器是否是 `const` 的。适用于需要修改容器内容的场景。`cbegin`：始终返回 `const` 迭代器，不能修改容器内容。适用于只读访问容器的场景。

---

2. `end` 和 `cend` 同理。

- Capacity

1. `empty` 返回 `vector` 是否为空。

---

2. `size` 返回 `vector` 中元素的数量。

---

3. `capacity` 返回在不重新分配内存的情况下，`vector` 可以容纳的元素数量。

---

4. `reserve` 请求分配至少容纳 `n` 个元素的内存。如果 `n` 小于当前容量，则不进行任何操作。

---

- Modifiers

1. `.clear()` 移除所有元素。

---

2. `insert` 在指定位置前插入元素。

```cpp
iterator insert( const_iterator pos, T&& value );
iterator insert( const_iterator pos, size_type count, const T& value );
iterator insert( const_iterator pos, InputIt first, InputIt last );
```

- 在 `pos` 前插入 `value`
- 在 `pos` 前插入 `count` 个 `value`
- 在 `pos` 前插入来自范围 `[first, last)` 的元素

---

3. `erase` 移除指定位置的元素。

```cpp
iterator erase( iterator pos );
iterator erase( iterator first, iterator last );
```

- 移除位于 `pos` 的元素。
- 移除范围 `[first, last)` 中的元素。
- 返回值是最后移除元素之后的迭代器。
    - 如果 `pos` 指代末元素，那么返回 `end()` 迭代器。
    - 如果在移除前 `last == end()`，那么返回更新的 `end()` 迭代器。如果范围 `[first, last)` 为空，那么返回 `last`。

---

4. `push_back` 追加给定元素 `value` 到容器尾。

```cpp
void push_back( T&& value );
```

---

```cpp
#include <iostream>
#include <vector>
using namespace std;

int main(){
    vector<int> evens {2, 4, 6, 8};
    evens.push_back(20);
    evens.push_back(22);
    evens.insert(evens.begin()+4, 5, 10);

    for(int i = 0; i < evens.size(); i++){
        cout << evens[i] << " ";
    }
    cout << endl;

    for(vector<int>::iterator it = evens.begin(); it < evens.end(); it++){  

        // 每个容器下面都有这个迭代器 iterator 
        // 使用要解引用，因为这个底层就是用指针写的

        cout << *it << " ";
    }
    cout << endl;

    for(int e: evens){  
        
        // range-based for loop 如果只需要访问里面的元素的话

        cout << e << " ";
    }
    cout << endl;

    for(auto it = evens.begin(evens); it < evens.end(); it++){  
        
        // 上面相当于在做这个
        
        cout << *it << " ";
    }
    cout << endl;

    return 0;
}
```

###### Pitfalls - access safety

Accessing an invalid element of a vector.

```cpp
vector<int> v;
v[100] = 1; // Whoops!
```

- use `push_back()` for dynamic expansion.
- Preallocate with constructor.
- Reallocate with resize() .

---

###### Pitfalls - size() on list<>

- This might cost linear time before C++11.

```cpp
if (my_list.size() == 0) {
 ...
}
```

- **Constant time guaranteed**.

```cpp
if (my_list.empty()) {
 ...
}
```

---

###### Pitfalls - invalid iterator

```cpp
list<int> L;
list<int>::iterator li;
li = L.begin();
L.erase(li);
++li; // WRONG because it is a list 链表连接
```

- Using invalid iterator.
- `li` 初始指向链表 L 的第一个元素（`L.begin()`）。
- `L.erase(li)` 删除了 `li` 所指向的元素。
- 删除操作后，`li` 变为无效的迭代器（因为它指向的元素已经被删除）。
- 尝试对无效的迭代器 `li` 进行 `++li` 操作是未定义行为，可能导致程序崩溃或错误。

```cpp
li = L.erase(li); // RIGHT
```

- Use return value of `erase()` to advance.
- `L.erase(li)` 会删除 `li` 所指向的元素，并返回一个指向下一个有效元素的迭代器。
- 将返回值赋值给 `li`，这样 `li` 仍然是一个有效的迭代器，指向删除操作后的下一个元素。可以安全地继续使用 `li`。


!!! note "vector[] vs at()"
    `operator[]` 不进行边界检查。如果索引越界，行为是未定义的。更快，因为没有额外的边界检查开销。

    `at()` 进行边界检查。如果索引越界，抛出 std::out_of_range 异常。稍慢，因为需要进行边界检查。

###### `std::vector` 的迭代器

类型：`std::vector` 的迭代器是随机访问迭代器（Random Access Iterator）。

1. 支持的操作：

- 向前遍历（`++p`）。
- 向后遍历（`--p`）。
- 随机访问（`p + n` 或 `p - n`）。
- 比较大小（`p1 < p2` 或 `p1 > p2`）。

**原因**： `std::vector` 的底层实现是动态数组，元素在内存中是连续存储的，因此可以通过指针算术快速访问任意位置的元素（时间复杂度为 O(1)）。

---

##### `list`

###### `std::list` 的迭代器是**双向迭代器**（Bidirectional Iterator）。

1. 支持的操作：

- 向前遍历（++p）。
- 向后遍历（--p）。
- 比较是否相等（p1 == p2 或 p1 != p2）。

2. 不支持的操作：

- 随机访问（`p + n` 或 `p - n`）。
- 比较大小（`p1 < p2` 或 `p1 > p2`）。

**原因**：`std::list` 的底层实现是双向链表，元素在内存中不是连续存储的，因此无法通过简单的指针算术快速访问任意位置的元素。

---

#### Associative

- `set` (collection of unique keys)
- `map` (collection of key-value pairs)
- `multiset` , `multimap`

##### `map`

- Collection of key-value pairs.
- Lookup by key, and retrieve a value.
- Example: a telephone book, `map<string,string>`

`std::map` 是一种有序关联容器，它包含具有唯一键的键值对。键之间以比较函数 `Compare` 排序。搜索、移除和插入操作拥有对数复杂度。`map` 通常实现为红黑树。

```cpp
#include <iostream>
#include <map>
#include <string>
using namespace std;

int main(){
    map<string, int> price;
    price["apple"] = 3;
    price["orange"] = 5;
    price["banana"] = 1;

    for(const auto &pair: price){
        cout << "{" << pair.first << " : " << pair.second << "} ";  
        
        // 其中的一个元素是 pair<string, int>
    }
    cout << endl;

    string item;
    int total = 0;
    while(cin >> item){
        total += price[item];
    }
    cout << total << endl;

    while(cin >> item){
        if(price.contains(item)){
            total += price[item];
        }else{
            cout << "No such item: " << item << endl;
        }
    }
}
```

!!! note "关于 map 的访问"
    1. 使用 `operator[]` 访问

    如果键不存在，`std::map` 会自动插入该键，并将其值初始化为默认值（对于基本类型，如 `int`，默认值为 `0`；对于类类型，调用默认构造函数）。再返回该键对应的值的引用。

    2. 使用 `at()` 访问

    如果键不存在，`at()` 会抛出 `std::out_of_range` 异常。不会修改 `std::map`。

    3. 使用 `find()` 访问

    如果键不存在，`find()` 返回 `std::map::end()`，表示未找到。不会修改 `std::map`。

---

###### 结构化绑定

```cpp
#include <iostream>
#include <map>
#include <string>
using namespace std;

int main(){
    map<string, int> word_map;
    for(const auto& w : {"we", "are", "not", "humans", "we", "are", "robots", "!!"}){
        ++word_map[w];
    }

    for(const auto& [word, count] : word_map){  // [] 是结构化的绑定
        cout << word << " occurs " << count << " times" << endl;
    }

    return 0;
}
```

- `word_map` 是一个 `std::map<std::string, int>`，它的元素类型是 `std::pair<const std::string, int>`。
- `const auto& [word, count]` 是结构化绑定：
    - `word` 绑定到 `std::pair` 的第一个成员（即键，`std::string` 类型）。
    - `count` 绑定到 `std::pair` 的第二个成员（即值，`int` 类型）。
    - 这样，你可以直接使用 `word` 和 `count`，而不需要通过 `pair.first` 和 `pair.second` 来访问。

---

|name|phone|
|:---:|:---:|
|"Charles Nguyen"|"(531) 9392 4587"|
|"Lisa Jones"|"(402) 4536 4674"|
|"William H. Smith"|"(998) 5488 0123"|

##### Pitfalls - silent insertion

- Inadvertently inserting into `map<>`

```cpp
if (foo["bob"] == 1) // create an entry "bob" silently
```

- Use `count()` , or `contains()` , to check for a key without creating a new entry.

```cpp
if (foo.count("bob"))
if (foo.contains("bob")) // introduced in C++20
```

---

#### Unordered associative

- hashed by keys
- `unordered_set` , `unordered_map`
- `unordered_multiset` , `unordered_multimap`

---

#### Adaptors

- `stack` , `queue` , `priority_queue`

```cpp
#include <iostream>
#include <stack>
#include <string>
#include <vector>
#include <deque>
using namespace std;

template <typename T> 
class Stack{
public:
    virtual ~Stack() = default;
    virtual T& top() = 0;
    virtual bool empty() const = 0;
    virtual size_t size() const = 0;
    virtual void push(const T& value) = 0;
    virtual void pop() = 0;
};

template <typename T, typename Container = std::deque<T>>
class c_stack : public Stack<T>{
pubulic:
    T& top() override{ return c.back();}
    bool empty() const override{ return c.empty();}
    size_t size() const override{ return c.size();}
    void push(const T& value) override{ c.push_back(value);}
    void pop() override{ c.pop_back();}
Private:
    Container c;
};

bool is_balanced(const string& s){
    c_stack<char, list<char>> st;

    for(char c : s){
        if(c == '(' || c == '{' || c == '['){
            st.push(c);
        }else if(c == ')' || c == '}' || c == ']'){
            if(st.empty()) return false;
            char top = st.top();
            st.pop();
            if((c == ')' && top != '(') || (c == '}' && top != '{') || (c == ']' && top != '[')){
                return false;
            }
        }
    }

    return st.empty();
}

int main(){
    string test1 = "a(b{c[d]e}f)g";
    string test2 = "x(y{z[)}}";

    cout << "Test 1: " << (is_balanced(test1) ? "Balanced" : "Unbalanced") << endl;
    cout << "Test 2: " << (is_balanced(test2) ? "Balanced" : "Unbalanced") << endl;

    return 0;
}
```

- **纯虚函数**

将成员函数声明为 纯虚函数(即使用 = 0)的目的是定义一个 抽象基类(接口类)，强制派生类必须实现这些函数。纯虚函数没有默认实现，要求所有派生类必须提供具体实现。这相当于定义了一个 接口规范，强制所有子类遵循统一的接口设计。

---

```cpp
#include <iostream>
#include <vector>
#include <infix_iterator.h>

int main(){
    vector<int> v = {1, 2, 3, 5};
    vector<int> u;

    reverse(v.begin(), v.end());
    copy(v.begin(), v.end(), u.begin()); // 这会跑崩
    copy(v.begin(), v.end(), back_inserter(u));

    copy(u.begin(),u.end(),ostream_iterator<int>(cout, ",")); // 5,3,2,1,
    cout << endl;

    list<int> l;
    copy(v.begin(), v.end(), front_inserter(l));
    copy(l.begin(), l.end(), ostream_iterator<int>(cout, ",")); // 1,2,3,5,
    cout << endl;

    copy(v.begin(), v.end(), infix_ostream_iterator<int>(cout, ","));  // 1,2,3,5
    cout << endl;
}
```

- `copy(v.begin(), v.end(), u.begin());` 

`u` 是一个空向量，`u.begin()` 指向无效内存位置。`copy` 试图向未分配内存的位置写入数据，导致未定义行为（程序崩溃或数据损坏）。

- `std::back_inserter`

插入迭代器适配器，通过 `push_back` 向容器末尾添加元素。

- `std::copy(u.begin(), u.end(), std::ostream_iterator<int>(std::cout, ","));`

输出迭代器，将元素写入输出流（如 std::cout）。可以不用循环。

输出：5,3,2,1,（注意末尾多余的逗号）。

- `copy(v.begin(), v.end(), front_inserter(l));`

插入迭代器适配器，通过 `push_front` 向容器头部添加元素。

`std::copy` 按原顺序复制元素，但 `front_inserter` 会逆序插入（因为每次插入到头部）。

- `copy(v.begin(), v.end(), infix_ostream_iterator<int>(cout, ","));`

仅在元素之间插入分隔符（避免末尾多余的分隔符）。

---

### Algorithms

!!! note
    有关 Algorithms 的详细内容，可以看 [105 STL Algorithmsin Less Than an Hour](https://melody12020831.github.io/Notebook/Computer_Science/OOP/105_STL_Algorithmsin_Less_Than_an_Hour)

---

### Iterators

#### Typedefs

- Annoying to type long names
    - `map<Name,list<PhoneNum>> phonebook ;`
    - `map<Name,list<PhoneNum>>::iterator finger ;`
- Simplify with typedef
    - `typedef map<Name,list<PhoneNum>> PB ;`
    - `PB phonebook ;`
    - `PB::iterator finger ;`
- C++11: `auto` , `using`

**Using your own classes**

- Might need:
    - assignment operator, `operator=()`
    - default constructor
- For sorted types, like `set` , `map` , ...
    - less-than operator, `operator<()`

---

## Further reading

<div class="card file-block" markdown="1">
<div class="file-icon"><img src="/Notebook/assets/images/pdf.svg" style="height: 3em;"></div>
<div class="file-body">
<div class="file-title"> introducing-the-stl </div>
<div class="file-meta"> 93 KB / 2025-03-03</div>
</div>
<a class="down-button" target="_blank" href="/Notebook/Computer_Science/OOP/Further_reading/[Further Readings] introducing-the-stl.pdf" markdown="1">:fontawesome-solid-download: 下载</a>
</div>

---