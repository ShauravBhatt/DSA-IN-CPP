
# Functions Continued: Scope, Pass By Reference & Default Parameters

# Scope of Variables

## What is Scope?

Scope defines:

```text
Where can a variable be accessed?
```

or

```text
Kis area mein variable visible hai?
```

Think of scope as the **boundary or ownership area** of a variable.

---

# Types of Scope

```text
1. Global Scope
2. Local Scope
3. Block Scope
```

---

# 1. Global Scope

A variable declared outside all functions is called a **Global Variable**.

Example:

```cpp
#include <iostream>
using namespace std;

int globalVar = 100;

void display()
{
    cout << globalVar << endl;
}

int main()
{
    cout << globalVar << endl;

    display();

    return 0;
}
```

Output:

```text
100
100
```

---

## Why?

Because:

```text
globalVar
```

was declared outside every function.

So:

```text
main()      ✅ Access

display()   ✅ Access

any function ✅ Access
```

---

# Memory View

```text
Global Memory

-----------------
globalVar = 100
-----------------
```

Every function can see it.

---

# 2. Local Scope

A variable declared inside a function.

Example:

```cpp
void display()
{
    int x = 10;
}
```

Here:

```text
x
```

belongs only to:

```text
display()
```

---

Example:

```cpp
#include <iostream>
using namespace std;

void display()
{
    int x = 10;

    cout << x << endl;
}

int main()
{
    display();

    return 0;
}
```

Valid.

---

But:

```cpp
#include <iostream>
using namespace std;

void display()
{
    int x = 10;
}

int main()
{
    cout << x;
}
```

Error ❌

Because:

```text
x only exists inside display()
```

---

# 3. Block Scope

A variable declared inside a block `{}`.

Example:

```cpp
#include <iostream>
using namespace std;

int main()
{
    if(true)
    {
        int age = 20;

        cout << age << endl;
    }

    cout << age << endl;

    return 0;
}
```

Error ❌

Because:

```text
age only belongs to the if block
```

---

Visual:

```text
main()
{
    if(true)
    {
        age = 20
    }
}
```

Scope of age:

```text
Only inside { }
```

---

# One Program Covering Everything

```cpp
#include <iostream>
using namespace std;

int globalVar = 100;

void display()
{
    int localDisplay = 50;

    cout << "Global : "
         << globalVar << endl;

    cout << "Local Display : "
         << localDisplay << endl;
}

int main()
{
    int localMain = 10;

    cout << globalVar << endl;

    display();

    if(true)
    {
        int blockVar = 20;

        cout << blockVar << endl;
    }

    return 0;
}
```

---

# Accessibility Table

| Variable | Global | display() | main() | if Block |
|----------|---------|------------|---------|----------|
| globalVar | ✅ | ✅ | ✅ | ✅ |
| localDisplay | ❌ | ✅ | ❌ | ❌ |
| localMain | ❌ | ❌ | ✅ | ❌ |
| blockVar | ❌ | ❌ | ❌ | ✅ |

---

# Scope Rule

```text
Global Variable

Visible Everywhere
```

```text
Local Variable

Visible Only Inside Function
```

```text
Block Variable

Visible Only Inside Block
```

---

# Pass By Reference

Last chapter:

```text
Pass By Value

Function gets a COPY
```

Now:

```text
Pass By Reference

Function gets ORIGINAL variable
```

This means:

```text
Changes inside function

WILL affect original variable
```

---

# Before Learning Pass By Reference

You must understand:

```text
1. Memory Address
2. Address Operator (&)
3. Reference
```

---

# Memory Address

Every variable gets a location in RAM.

Example:

```cpp
int x = 10;
```

Memory:

```text
Address     Value

1000        10
```

(Address is just an example)

---

# Address Operator (&)

Used to get memory address.

Example:

```cpp
#include <iostream>
using namespace std;

int main()
{
    int x = 10;

    cout << &x;

    return 0;
}
```

Output:

```text
0x61ff08
```

(Address varies every run)

---

# Reference

A reference is simply another name for the same variable.

Syntax:

```cpp
datatype &referenceName = variable;
```

Example:

```cpp
int x = 10;

int &ref = x;
```

Now:

```text
x
```

and

```text
ref
```

point to same memory.

---

Visual

```text
Memory

Address      Value

1000         10
 ↑
 x
 ↑
 ref
```

Both names refer to same variable.

---

Example

```cpp
int x = 10;

int &ref = x;

ref = 50;

cout << x;
```

Output:

```text
50
```

Why?

Because:

```text
ref and x are same variable
```

---

# Pass By Reference Syntax

```cpp
void update(int &num)
{
}
```

Notice:

```cpp
&
```

This is what makes it reference.

---

# Example Program

```cpp
#include <iostream>
using namespace std;

void updateValue(int &num)
{
    num = num + 100;
}

int main()
{
    int x = 10;

    cout << "Before : "
         << x << endl;

    updateValue(x);

    cout << "After : "
         << x << endl;

    return 0;
}
```

Output:

```text
Before : 10

After : 110
```

---

# Why Did It Change?

Pass By Value:

```text
Copy Sent
```

```cpp
updateValue(10)
```

Changes disappear.

---

Pass By Reference:

```text
Original Variable Sent
```

Function directly modifies:

```text
x
```

inside main.

---

# Memory View

Before:

```text
x = 10
```

Call:

```cpp
updateValue(x);
```

Inside function:

```text
num and x

same memory location
```

Update:

```cpp
num = 110;
```

Now:

```text
x = 110
```

also changes.

---

# Pass By Value vs Pass By Reference

| Feature | Pass By Value | Pass By Reference |
|----------|--------------|------------------|
| Copy Created | ✅ | ❌ |
| Original Changes | ❌ | ✅ |
| Extra Memory | More | Less |
| Safe Modification | ✅ | ❌ |
| Fast for Large Data | ❌ | ✅ |

---

# Default Parameters

Sometimes user may not provide all values.

In such cases we can keep default values.

---

Example

```cpp
void greet(string name = "Guest")
{
    cout << "Hello "
         << name;
}
```

---

Call 1

```cpp
greet();
```

Output:

```text
Hello Guest
```

---

Call 2

```cpp
greet("Shaurav");
```

Output:

```text
Hello Shaurav
```

---

# Another Example

```cpp
int multiply(int a, int b = 2)
{
    return a * b;
}
```

---

Call:

```cpp
multiply(5);
```

Output:

```text
10
```

Because:

```text
b automatically becomes 2
```

---

Call:

```cpp
multiply(5,4);
```

Output:

```text
20
```

Because:

```text
Provided value overrides default value.
```

---

# Complete Program

```cpp
#include <iostream>
using namespace std;

int multiply(int a, int b = 2)
{
    return a * b;
}

int main()
{
    cout << multiply(5) << endl;

    cout << multiply(5,4);

    return 0;
}
```

Output:

```text
10
20
```

---

# Rules of Default Parameters

Valid:

```cpp
int func(int a,
         int b = 10,
         int c = 20);
```

---

Invalid:

```cpp
int func(int a = 10,
         int b,
         int c = 20);
```

❌ Error

---

Rule:

```text
Default parameters must be assigned
from Right → Left.
```

---

# Final Revision

## Scope

```text
Global Scope
→ Accessible Everywhere

Local Scope
→ Accessible Inside Function

Block Scope
→ Accessible Inside Block {}
```

---

## Pass By Reference

```cpp
void update(int &x)
```

Meaning:

```text
Function receives original variable.
```

Changes reflect in caller.

---

## Address Operator

```cpp
&x
```

Gives memory address of x.

---

## Reference

```cpp
int &ref = x;
```

Creates another name for same variable.

---

## Default Parameters

```cpp
int multiply(int a, int b = 2);
```

Used when caller doesn't provide value.

---

# 80/20 Takeaway

Remember only these 5 lines:

```text
1. Global variables are visible everywhere.

2. Local variables belong to their function.

3. Block variables belong to their block {}.

4. Pass By Value sends a copy.

5. Pass By Reference sends the original variable.
```