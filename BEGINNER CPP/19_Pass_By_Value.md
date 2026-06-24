# Functions Continued: Pass By Value, Scope & Practical Examples

---

# Pass By Value

## What is Pass By Value?

By default, C++ function arguments are passed using **Pass By Value**.

This means:

```text
Function ko original variable nahi diya jata.

Us variable ki COPY di jaati hai.
```

---

## Example

```cpp
#include <iostream>
using namespace std;

void changeNumber(int num)
{
    num = 100;
}

int main()
{
    int x = 10;

    changeNumber(x);

    cout << x;

    return 0;
}
```

Output:

```text
10
```

Not:

```text
100
```

---

# Why?

Let's understand memory.

Initially:

```text
main()

x = 10
```

Memory:

```text
----------------
x = 10
----------------
```

---

Function Call:

```cpp
changeNumber(x);
```

During call:

```text
Copy of x is created
```

Function Frame:

```text
----------------
num = 10
----------------
```

Notice:

```text
x and num are different variables.
```

Even though they contain the same value initially.

---

Function Execution

```cpp
num = 100;
```

Now memory becomes:

```text
main()

x = 10
```

```text
changeNumber()

num = 100
```

---

Function Ends

```text
changeNumber() frame destroyed
```

Only:

```text
x = 10
```

survives.

Therefore output:

```text
10
```

---

# Golden Rule

```text
Pass By Value

Original Variable ❌

Copy of Variable ✅
```

Changes made inside function:

```text
Do NOT affect original variable.
```

---

# Visual Representation

```text
main()
|
|-- x = 10
|
|-- changeNumber(x)
      |
      |-- num = 10 (copy)
      |
      |-- num = 100
      |
      |-- function ends
|
|-- x still 10
```

---

# When Is Pass By Value Useful?

When:

```text
✓ We don't want original data to change.

✓ Function only needs to read data.

✓ Safer programming.
```

Example:

```cpp
calculateArea(length, width);
```

Function only calculates.

No need to modify original values.

---

# Example 1: Sum of Digits Using Function

Problem:

```text
Input: 1234

Output: 10

Because:

1 + 2 + 3 + 4 = 10
```

---

## Logic

To extract digits:

```cpp
digit = n % 10;
```

To remove last digit:

```cpp
n = n / 10;
```

---

## Code

```cpp
#include <iostream>
using namespace std;

int sumOfDigits(int number)
{
    int sum = 0;

    while(number > 0)
    {
        int digit = number % 10;

        sum += digit;

        number = number / 10;
    }

    return sum;
}

int main()
{
    int n;

    cout << "Enter Number: ";
    cin >> n;

    cout << "Sum of Digits = "
         << sumOfDigits(n);

    return 0;
}
```

---

# Dry Run

Input:

```text
1234
```

Iteration 1:

```text
digit = 4

sum = 4

number = 123
```

---

Iteration 2:

```text
digit = 3

sum = 7

number = 12
```

---

Iteration 3:

```text
digit = 2

sum = 9

number = 1
```

---

Iteration 4:

```text
digit = 1

sum = 10

number = 0
```

Loop Ends.

Output:

```text
10
```

---

# Example 2: Binomial Coefficient (nCr)

Formula:

```text
nCr = n! / (r! × (n-r)!)
```

Example:

```text
5C2

= 5! / (2! × 3!)

= 120 / (2 × 6)

= 10
```

---

# Step 1: Create Factorial Function

```cpp
int factorial(int n)
{
    int fact = 1;

    for(int i = 1; i <= n; i++)
    {
        fact *= i;
    }

    return fact;
}
```

---

# Step 2: Create nCr Function

```cpp
int nCr(int n, int r)
{
    int numerator = factorial(n);

    int denominator =
        factorial(r) *
        factorial(n-r);

    return numerator / denominator;
}
```

Notice:

```text
nCr() is using factorial()

Function Calling Function
```

This is extremely common in programming.

---

# Complete Program

```cpp
#include <iostream>
using namespace std;

int factorial(int n)
{
    int fact = 1;

    for(int i = 1; i <= n; i++)
    {
        fact *= i;
    }

    return fact;
}

int nCr(int n, int r)
{
    int numerator = factorial(n);

    int denominator =
        factorial(r) *
        factorial(n-r);

    return numerator / denominator;
}

int main()
{
    int n, r;

    cout << "Enter n: ";
    cin >> n;

    cout << "Enter r: ";
    cin >> r;

    cout << "nCr = "
         << nCr(n, r);

    return 0;
}
```

---

# Execution Flow

Suppose:

```text
n = 5

r = 2
```

Main:

```cpp
nCr(5,2)
```

Inside nCr:

```cpp
factorial(5)
```

returns:

```text
120
```

---

Then:

```cpp
factorial(2)
```

returns:

```text
2
```

---

Then:

```cpp
factorial(3)
```

returns:

```text
6
```

---

Final:

```text
120 / (2 × 6)

120 / 12

10
```

Output:

```text
10
```

---

# Scope of Variables

## What is Scope?

Scope defines:

```text
"Where a variable can be accessed?"
```

or

```text
"Kis area mein variable visible hai?"
```

---

# Local Scope

Variable function ke andar create hua.

Sirf us function ke andar accessible hoga.

Example:

```cpp
#include <iostream>
using namespace std;

void test()
{
    int x = 10;

    cout << x;
}

int main()
{
    test();

    return 0;
}
```

Valid.

---

But:

```cpp
#include <iostream>
using namespace std;

void test()
{
    int x = 10;
}

int main()
{
    cout << x;
}
```

Error.

Because:

```text
x only belongs to test()
```

---

# Visual Understanding

```text
main()
{
    int a = 10;
}
```

Scope:

```text
Only inside main()
```

---

```cpp
void display()
{
    int b = 20;
}
```

Scope:

```text
Only inside display()
```

---

# Why Local Scope Is Important?

Imagine:

```cpp
login()

displayProfile()

logout()
```

All functions use:

```cpp
int count;
```

If everything were shared:

```text
Huge confusion
```

Local scope gives:

```text
Isolation

Safety

Better Maintenance
```

Each function gets its own private workspace.

---

# 80/20 Takeaway

If you remember only four things from this chapter:

```text
1. Functions get copies of variables by default
   (Pass By Value)

2. return sends data back to caller

3. Functions can call other functions

4. Variables created inside a function
   stay inside that function only
   (Local Scope)
```

These four ideas form the foundation for the next big topic:

```text
🔥 Pass By Reference

🔥 References (&)

🔥 Memory Addresses

🔥 Recursion
```

Once Pass By Reference clicks, you'll finally understand why some functions can modify variables in `main()` and some cannot.