# Loops in C++ 

## Introduction

Loops ka use tab kiya jaata hai jab hume kisi block of code ko multiple times execute karna ho.

Without loops:

```cpp
cout << 1 << endl;
cout << 2 << endl;
cout << 3 << endl;
cout << 4 << endl;
cout << 5 << endl;
```

With loops:

```cpp
for(int i = 1; i <= 5; i++) {
    cout << i << endl;
}
```

---

# Types of Loops

1. `while` Loop
2. `do-while` Loop
3. `for` Loop

---

# 1. While Loop

## Syntax

```cpp
while(condition) {
    // code
}
```

## Flow

1. Condition check hoti hai.
2. Agar true hai → loop execute hota hai.
3. Fir condition dobara check hoti hai.
4. Jab condition false ho jaati hai → loop stop.


---

## Example 1: Print 1 to 5

```cpp
#include <iostream>
using namespace std;

int main() {
    int i = 1;

    while(i <= 5) {
        cout << i << endl;
        i++;
    }
}
```

Output:

```text
1
2
3
4
5
```

---

## Example 2: Countdown

```cpp
int n = 5;

while(n > 0) {
    cout << n << endl;
    n--;
}
```

Output:

```text
5
4
3
2
1
```

---

## Example 3: Infinite Loop

```cpp
while(true) {
    cout << "Hello";
}
```

⚠️ Never stops.

---

## When to Use While?

Use when:

- Number of iterations is unknown.
- Loop depends on a condition.
- Input validation.
- Menu-driven programs.

Example:

```cpp
while(password != correctPassword)
```

---

# 2. Do-While Loop

## Syntax

```cpp
do {
    // code
}
while(condition);
```

## Flow

1. Loop body executes first.
2. Then condition is checked.
3. If true → repeat.
4. If false → stop.

### Key Point

✅ Executes at least once.

---

## Example 1

```cpp
int i = 1;

do {
    cout << i << endl;
    i++;
}
while(i <= 5);
```

Output:

```text
1
2
3
4
5
```

---

## Example 2: Condition False Initially

```cpp
int i = 10;

do {
    cout << i;
}
while(i < 5);
```

Output:

```text
10
```

Notice:

Condition false thi, phir bhi ek baar execute hua.

---

## Example 3: Menu Program

```cpp
int choice;

do {
    cout << "1. Tea\n";
    cout << "2. Exit\n";

    cin >> choice;

} while(choice != 2);
```

---

## When to Use Do-While?

Use when:

- At least one execution required ho.
- Menus.
- User input systems.
- Retry systems.

Example:

```cpp
do {
    cin >> password;
}
while(password != correctPassword);
```

---

# 3. For Loop

## Syntax

```cpp
for(initialization; condition; update) {
    // code
}
```

---

## Structure

```cpp
for(int i = 1; i <= 5; i++)
```

### Initialization

Runs once.

```cpp
int i = 1;
```

### Condition

Runs before every iteration.

```cpp
i <= 5
```

### Update

Runs after every iteration.

```cpp
i++
```

---

## Example 1: Print 1 to 5

```cpp
for(int i = 1; i <= 5; i++) {
    cout << i << endl;
}
```

Output:

```text
1
2
3
4
5
```

---

## Example 2: Reverse Counting

```cpp
for(int i = 10; i >= 1; i--) {
    cout << i << endl;
}
```

Output:

```text
10
9
8
7
6
5
4
3
2
1
```

---

## Example 3: Sum of Numbers

```cpp
int sum = 0;

for(int i = 1; i <= 5; i++) {
    sum += i;
}

cout << sum;
```

Output:

```text
15
```

---

# Nested Loops

A loop inside another loop.

```cpp
for(int i = 1; i <= 3; i++) {

    for(int j = 1; j <= 3; j++) {
        cout << "* ";
    }

    cout << endl;
}
```

Output:

```text
* * *
* * *
* * *
```

Used in:

- Patterns
- Matrices
- Grids
- Tables

---

# break Statement

Immediately exits loop.

```cpp
for(int i = 1; i <= 10; i++) {

    if(i == 5)
        break;

    cout << i << endl;
}
```

Output:

```text
1
2
3
4
```

---

# continue Statement

Skips current iteration.

```cpp
for(int i = 1; i <= 5; i++) {

    if(i == 3)
        continue;

    cout << i << endl;
}
```

Output:

```text
1
2
4
5
```

---

# Which Loop Should You Use?

## While Loop

Use when:

- Iterations unknown.
- Condition-based execution.

Examples:

- Password checking
- User input validation
- Reading files

---

## Do-While Loop

Use when:

- Code must run at least once.

Examples:

- Menus
- Login retries
- User confirmation systems

---

## For Loop

Use when:

- Iterations known.

Examples:

- Arrays
- Counting
- Mathematical calculations
- Pattern printing

---

# Quick Comparison

| Feature | while | do-while | for |
|----------|----------|----------|----------|
| Condition checked first | ✅ | ❌ | ✅ |
| Executes at least once | ❌ | ✅ | ❌ |
| Best for unknown iterations | ✅ | ✅ | ❌ |
| Best for counting | ❌ | ❌ | ✅ |
| Most commonly used | ✅ | ❌ | ✅ |

---

# Common Mistakes

## 1. Infinite Loop

```cpp
int i = 1;

while(i <= 5) {
    cout << i;
}
```

❌ Forgot:

```cpp
i++;
```

---

## 2. Wrong Condition

```cpp
for(int i = 1; i >= 5; i++)
```

Loop never runs.

---

## 3. Semicolon After Loop

```cpp
while(i <= 5);
{
    cout << i;
}
```

❌ Infinite loop.

---
