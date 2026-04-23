---
statistics: True
comments: true
---

# HW6

## 6.3

???+ question
    For each of the variables a, b, c, d, e in this C program, say whether the variable should be kept in memory or a register, and why.

    ```c
    int f(int a, int b)
    { 
        int c[3], d, e;
        d=a+1;
        e=g(c, &b);
        return e+c[1]+b;
    }
    ```

??? note "answer"
    1. a: register, because its value only needs to be read once for calculation, it does not require a memory address.

    2. b: memory, because there is `e=g(c, &b);`. Function g might internally read or modify the value at this address via a pointer. Registers do not have addresses, therefore b cannot exist solely in a register.

    3. c: memory, because arrays require a contiguous block of memory to support memory offset-based access like c[1]. And when c is passed to function g, its base address is passed, which means that the external function expects it to exist in memory.

    4. d: register, because d is a simple local variable that is not addressed, and will be allocated in a register.

    5. e: register, because its value is computed from c and b and used only once. And e is not taken at the address and it merely acts as a temporary variable.

---

## 6.7(a,b)

???+ question
    A display is a data structure that may be used as an alternative to static links for maintaining access to nonlocal variables. It is an array of frame pointers, indexed by static nesting depth. Element $D_i$ of the display always points to the most recently called function whose static nesting depth is i.

    The bookkeeping performed by a function f , whose static nesting depth is i, looks like:

    ```
    Copy $D_i$ to save location in stack frame
    Copy frame pointer to $D_i$
    ··· body of f ···
    Copy save location back to $D_i$
    ```

    In Program 6.3, function prettyprint is at depth 1, write and show are at depth 2, and so on.

    a. Show the sequence of machine instructions required to fetch the variable output into a register at line 14 of Program 6.3, using static links.

    b. Show the machine instructions required if a display were used instead.

    PROGRAM 6.3. Nested functions.

    ```c
    type tree = {key: string, left: tree, right: tree}

    function prettyprint(tree: tree) : string =
        let
            var output := ""

            function write(s: string) =
                output := concat(output,s)

            function show(n:int, t: tree) =
                let function indent(s: string) =
                    (for i := 1 to n
                        do write(" ");
                    output := concat(output,s); write("\n"))
                in if t=nil then indent(".")
                    else (indent(t.key);
                        show(n+1,t.left);
                        show(n+1,t.right))
                end

        in show(0,tree); output
    end
    ```

??? note "answer"
    Depth 1: Function `prettyprint`. The variable `output` is defined at this level.

    Depth 2: Functions `write` and `show`, defined inside `prettyprint`.

    Depth 3: Function `indent`, defined inside `show`.

    a. 
    
    Current execution depth: $d_{current} = 3$ (belongs to indent).

    Target variable depth: $d_{target} = 1$ (a local variable output belonging to prettyprint).

    Therefore, the machine instruction sequence is as follows:

    1. Retrieve a pointer to the `show` stack frame from the current `indent` stack frame.

    2. Retrieve a pointer to the `prettyprint` stack frame from the `show` stack frame.

    3. Now $r_1$ points to the frame of prettyprint, and the value of output is read into the destination register by offset.

    b. 

    The target variable `output` exists in `prettyprint`, and the static depth of `prettyprint` is $1$.

    1. The frame pointer of prettyprint is loaded directly from the depth 1 index of the Display array.

    2. Read the output using the frame pointer and offset of prettyprint.

---