---
statistics: True
comments: true
---

# introduction

## The first CPP program

```cpp
#include<iostream>
using namespace std;
int main() {  
    int age;
    cin >> age;
    cout << "Hello, World! I am " << age << " years old!" << endl;  
    return 0;
}
```

- `iostream` 是定义输入/输出流相关函数和操作的头文件
- 命名空间用于区分具有相同方法名的代码块。在本程序中，使用命名空间 std; 将命名空间设置为标准，以便用户在程序中使用所有标准方法。
- 有些编译器 `void` 可能会报错，要用 `int`
- `cin` 是输入函数，`cout` 是输出函数
- `endl` 是换行符，相当于 `\n`
- 不写 `return 0` 也行
