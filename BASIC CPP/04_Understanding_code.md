# Understanding a Simple C++ Program

## Code

```cpp
#include <iostream>
using namespace std;

int main() {
    cout << "Hello Shaurav" << endl;
    return 0;
}
```

---

# 1. `#include <iostream>`

`#include` is a **preprocessor directive** that tells the compiler to include the contents of a header file before compilation.

```cpp
#include <iostream>
```

The `<iostream>` header provides input/output features such as:

```cpp
std::cout
std::cin
std::endl
```

### Why are Header Files Needed?

Headers contain declarations of functions, classes, and other components.

Examples:

| Header | Purpose |
|----------|----------|
| `<iostream>` | Input/Output |
| `<string>` | Strings |
| `<vector>` | Dynamic Arrays |
| `<cmath>` | Math Functions |
| `<fstream>` | File Handling |

Example:

```cpp
#include <string>

std::string name = "Shaurav";
```

Without `<string>`, the compiler wouldn't know what `std::string` is.

---

# 2. Namespaces

A **namespace** groups related identifiers and prevents naming conflicts.

Example:

```cpp
namespace A {
    void print() {}
}

namespace B {
    void print() {}
}
```

Calling:

```cpp
A::print();
B::print();
```

removes ambiguity because both functions have the same name.

---

## What is `std`?

Most of the C++ Standard Library lives inside:

```cpp
namespace std {
    ...
}
```

Examples:

```cpp
std::cout
std::cin
std::string
std::vector
```

---

## Ways to Use Namespaces

### 1. Fully Qualified (Recommended)

```cpp
std::cout << "Hello";
```

Clear and avoids conflicts.

---

### 2. Import Entire Namespace

```cpp
using namespace std;

cout << "Hello";
```

Convenient but can cause naming conflicts in large projects.

---

### 3. Import Specific Names

```cpp
using std::cout;
using std::endl;
```

Only selected names become directly accessible.

---

### 4. Namespace Alias

```cpp
namespace vln = very_long_namespace_name;

vln::display();
```

Useful for long namespace names.

---

# 3. `int main()`

```cpp
int main()
```

`main()` is the **entry point** of every C++ program.

When a program starts:

1. OS loads the executable.
2. Memory is allocated.
3. `main()` is called.
4. Program execution begins.

Example:

```cpp
void hello() {
    std::cout << "Hello";
}

int main() {
    hello();
}
```

Execution starts from `main()`, not `hello()`.

---

## Why `int`?

`main()` returns an integer exit code to the operating system.

```cpp
return 0;
```

means:

```text
Program executed successfully
```

Common convention:

| Return Value | Meaning |
|--------------|----------|
| `0` | Success |
| Non-zero | Error |

Modern C++ automatically inserts `return 0;` at the end of `main()` if omitted.

---

# 4. Curly Braces `{}`

Braces define a **scope**.

```cpp
int main() {
    int x = 10;
}
```

`x` only exists inside `main()`.

Outside:

```cpp
std::cout << x;
```

causes an error because `x` is out of scope.

---

# 5. `cout`

`cout` stands for:

```text
Character Output Stream
```

Used to display output on the console.

Example:

```cpp
std::cout << "Hello";
```

Output:

```text
Hello
```

Internally, `cout` is an object of type:

```cpp
std::ostream
```

---

# 6. Understanding `<<`

`<<` is called the **Stream Insertion Operator**.

```cpp
std::cout << "Hello";
```

means:

```text
Insert "Hello" into the output stream
```

---

## Original Meaning

`<<` is also the **left-shift operator**.

Example:

```cpp
4 << 1
```

Binary:

```text
0100 → 1000
```

Result:

```cpp
8
```

For streams, the operator is overloaded to perform output.

---

## Chaining

```cpp
std::cout << "Age: " << 20;
```

works because each `<<` returns the stream object, allowing another insertion.

---

# 7. `endl`

```cpp
std::endl
```

means **End Line**.

Example:

```cpp
std::cout << "Hello" << std::endl;
```

Output:

```text
Hello
```

and moves the cursor to the next line.

---

## `endl` vs `\n`

### Using `\n`

```cpp
std::cout << "Hello\n";
```

Adds a newline.

### Using `endl`

```cpp
std::cout << "Hello" << std::endl;
```

Adds a newline **and flushes the output buffer**.

Because flushing is slower, `\n` is often preferred unless immediate output is required.

---

# 8. String Literal

```cpp
"Hello Shaurav"
```

is a **string literal**.

Examples:

```cpp
"Hello"
"C++"
"Programming"
```

String literals are stored in read-only memory by the compiler.

---

# Program Execution Flow

```text
1. Preprocessor includes <iostream>
2. Compiler compiles the code
3. OS loads executable into memory
4. OS calls main()
5. cout prints "Hello Shaurav"
6. endl inserts a newline
7. return 0 sends success status
8. Program terminates
```
