# C++ Basics: Tokens, Keywords, Identifiers, Literals, Operators & Punctuators

Before the compiler understands a C++ program, it breaks the code into small units called **tokens**.

Example:

```cpp
int age = 20;
```

Tokens:

```text
int
age
=
20
;
```

---

# 1. Tokens

A **token** is the smallest meaningful unit in a C++ program.

Example:

```cpp
int age = 20;
```

Contains the tokens:

| Token | Type |
|---------|---------|
| `int` | Keyword |
| `age` | Identifier |
| `=` | Operator |
| `20` | Literal |
| `;` | Punctuator |

Everything a C++ program is made of ultimately consists of tokens.

---

# 2. Keywords

Keywords are **reserved words** that have a predefined meaning in C++.

You cannot use them as variable or function names.

Examples:

```cpp
int
float
double
char
if
else
for
while
return
class
public
private
namespace
```

Example:

```cpp
int age = 20;
```

Here:

```cpp
int
```

is a keyword telling the compiler that `age` stores an integer.

❌ Invalid:

```cpp
int return = 5;
```

because `return` is a keyword.

---

# 3. Identifiers

Identifiers are names given by programmers to variables, functions, classes, etc.

Examples:

```cpp
age
name
studentCount
calculateSum
Employee
```

Example:

```cpp
int age = 20;
```

Here:

```cpp
age
```

is an identifier.

---

## Rules for Identifiers

### Valid

```cpp
age
_age
student1
totalMarks
```

### Invalid

```cpp
1age
student-name
class
```

Reasons:

- Cannot start with a digit.
- Cannot contain special characters like `-`.
- Cannot be a keyword.

---

# 4. Literals

Literals are fixed values written directly in code.

Example:

```cpp
int age = 20;
```

`20` is a literal.

---

## Integer Literals

```cpp
10
25
100
```

---

## Floating Point Literals

```cpp
3.14
10.5
0.99
```

---

## Character Literals

```cpp
'A'
'B'
'Z'
```

(single quotes)

---

## String Literals

```cpp
"Hello"
"Shaurav"
"C++"
```

(double quotes)

---

## Boolean Literals

```cpp
true
false
```

---

# 5. Operators

Operators perform operations on values.

Example:

```cpp
a + b
```

Here `+` is an operator.

---

## Arithmetic Operators

| Operator | Meaning |
|-----------|-----------|
| `+` | Addition |
| `-` | Subtraction |
| `*` | Multiplication |
| `/` | Division |
| `%` | Modulus |

Example:

```cpp
int sum = 10 + 5;
```

---

## Assignment Operator

```cpp
=
```

Example:

```cpp
int age = 20;
```

Assigns `20` to `age`.

---

## Relational Operators

Used for comparisons.

| Operator | Meaning |
|-----------|-----------|
| `==` | Equal |
| `!=` | Not Equal |
| `>` | Greater Than |
| `<` | Less Than |
| `>=` | Greater or Equal |
| `<=` | Less or Equal |

Example:

```cpp
if(age >= 18)
```

---

## Logical Operators

| Operator | Meaning |
|-----------|-----------|
| `&&` | AND |
| `||` | OR |
| `!` | NOT |

Example:

```cpp
if(age > 18 && age < 60)
```

---

## Increment & Decrement

```cpp
++
--
```

Example:

```cpp
count++;
count--;
```

---

## Stream Operators

```cpp
<<
>>
```

Example:

```cpp
cout << "Hello";
cin >> age;
```

- `<<` → Output (Stream Insertion)
- `>>` → Input (Stream Extraction)

---

# 6. Punctuators (Punctuation Symbols)

Punctuators help structure a C++ program.

Examples:

| Symbol | Purpose |
|----------|----------|
| `;` | Statement terminator |
| `{}` | Scope block |
| `()` | Function parameters |
| `[]` | Arrays |
| `,` | Separator |
| `:` | Labels / Access Specifiers |

---

## Semicolon `;`

Marks the end of a statement.

```cpp
int age = 20;
```

Without it:

```cpp
int age = 20
```

Compiler error.

---

## Curly Braces `{}`

Define a block or scope.

```cpp
int main() {
}
```

---

## Parentheses `()`

Used with functions and conditions.

```cpp
main()

if(age > 18)
```

---

## Square Brackets `[]`

Used for arrays.

```cpp
int arr[5];
```

---

# Breaking the Entire Program into Tokens

Program:

```cpp
#include <iostream>

using namespace std;

int main() {
    cout << "Hello Shaurav" << endl;
    return 0;
}
```

---

## Line 1

```cpp
#include <iostream>
```

Tokens:

```text
#
include
<
iostream
>
```

---

## Line 2

```cpp
using namespace std;
```

Tokens:

```text
using
namespace
std
;
```

---

## Line 3

```cpp
int main()
```

Tokens:

```text
int
main
(
)
```

---

## Line 4

```cpp
{
```

Token:

```text
{
```

---

## Line 5

```cpp
cout << "Hello Shaurav" << endl;
```

Tokens:

```text
cout
<<
"Hello Shaurav"
<<
endl
;
```

---

## Line 6

```cpp
return 0;
```

Tokens:

```text
return
0
;
```

---

## Line 7

```cpp
}
```

Token:

```text
}
```

