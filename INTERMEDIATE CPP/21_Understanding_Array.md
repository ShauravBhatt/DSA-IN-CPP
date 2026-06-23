# Arrays Fundamentals in C++

---

# What is an Array?

Array ek **data structure** hai jo hume same data type ki multiple values ko ek hi variable name ke andar store karne deta hai.

Without Array:

```cpp
int marks1 = 80;
int marks2 = 85;
int marks3 = 90;
int marks4 = 75;
int marks5 = 88;
```

Agar 100 students ke marks store karne ho to?

```text
100 alag variables banane padenge 😵
```

Practical nahi hai.

---

Using Array:

```cpp
int marks[5] = {80, 85, 90, 75, 88};
```

Ab saare marks ek hi naam ke andar store ho gaye:

```text
marks
```

---

# Why Do We Need Arrays?

Arrays use karne ke main reasons:

```text
✓ Multiple similar values store kar sakte hain

✓ Variable count reduce hota hai

✓ Loops ke saath easily work karte hain

✓ Code clean aur manageable banta hai
```

---

# Array Syntax

General Syntax:

```cpp
datatype arrayName[size];
```

Example:

```cpp
int numbers[5];
```

Breakdown:

```text
int      → Data Type

numbers  → Array Name

5        → Size
```

Meaning:

```text
Ye array 5 integers store kar sakta hai.
```

---

# Declaring an Array

Sirf memory reserve karna:

```cpp
int numbers[5];
```

Memory reserve ho gayi.

Lekin values abhi initialize nahi hui hain.

Local array hone par garbage values mil sakti hain.

---

# Initializing an Array

Declaration ke saath values bhi de sakte ho.

```cpp
int numbers[5] = {10, 20, 30, 40, 50};
```

Memory:

```text
Index     Value

0         10
1         20
2         30
3         40
4         50
```

---

# Initialization Without Giving Size

Compiler khud size calculate kar sakta hai.

```cpp
int numbers[] = {10, 20, 30, 40, 50};
```

Compiler count karega:

```text
5 Elements
```

Therefore:

```text
Size = 5
```

automatically.

---

# Partial Initialization

```cpp
int arr[5] = {10,20};
```

Result:

```text
Index     Value

0         10
1         20
2         0
3         0
4         0
```

Remaining elements automatically:

```text
0
```

ban jaate hain.

---

# Visual Representation of Array

Example:

```cpp
int arr[5] = {10,20,30,40,50};
```

Visualization:

```text
+----+----+----+----+----+
|10  |20  |30  |40  |50  |
+----+----+----+----+----+

  0    1    2    3    4
```

Har box ko bolte hain:

```text
Array Element
```

Aur niche wale numbers ko bolte hain:

```text
Index
```

---

# What is Contiguous Memory Allocation?

Array ka sabse important property.

Array elements memory mein:

```text
Ek ke baad ek continuously store hote hain.
```

Example:

```cpp
int arr[5];
```

Assume first element address:

```text
1000
```

Memory:

```text
Address     Element

1000        arr[0]
1004        arr[1]
1008        arr[2]
1012        arr[3]
1016        arr[4]
```

(Assume int = 4 bytes)

---

Notice:

```text
1000
1004
1008
1012
1016
```

Beech mein koi gap nahi.

Isko bolte hain:

```text
Contiguous Memory Allocation
```

---

# What is Indexing?

Array ke andar har element ka ek position number hota hai.

Us position ko bolte hain:

```text
Index
```

Example:

```cpp
int arr[5] = {10,20,30,40,50};
```

```text
Index     Value

0         10
1         20
2         30
3         40
4         50
```

---

# Why Does Indexing Start From 0?

Bahut common interview question.

Internally array address calculation use karta hai.

Formula:

```cpp
Address of arr[i] = Base Address + (i × Size of Data Type)
```

Example:

Base Address:

```text
1000
```

For:

```cpp
arr[0]
```

Calculation:

```text
1000 + (0 × 4)

= 1000
```

First element mil gaya.

---

For:

```cpp
arr[1]
```

```text
1000 + (1 × 4)

= 1004
```

Second element.

---

Agar indexing 1 se start hoti:

```cpp
arr[1]
```

to directly second location par jump ho jaate.

Isliye:

```text
First Element = Index 0
```

zyada efficient hai.

---

# Types of Arrays

Mainly:

```text
1. Single Dimensional Array (1D)

2. Multi-Dimensional Array (2D, 3D...)
```

---

# Single Dimensional Array (1D)

Normal array.

Example:

```cpp
int arr[5] = {10,20,30,40,50};
```

Visualization:

```text
+----+----+----+----+----+
|10  |20  |30  |40  |50  |
+----+----+----+----+----+

  0    1    2    3    4
```

---

# Multi-Dimensional Array

Array ke andar Array.

Most common:

```text
2D Array
```

Example:

```cpp
int matrix[2][3];
```

Meaning:

```text
2 Rows

3 Columns
```

Visualization:

```text
+----+----+----+
| 1  | 2  | 3  |
+----+----+----+
| 4  | 5  | 6  |
+----+----+----+
```

Code:

```cpp
int matrix[2][3] =
{
    {1,2,3},
    {4,5,6}
};
```

---

# Accessing Array Elements

Syntax:

```cpp
arrayName[index]
```

Example:

```cpp
int arr[5] = {10,20,30,40,50};
```

Access:

```cpp
cout << arr[0];
```

Output:

```text
10
```

---

```cpp
cout << arr[3];
```

Output:

```text
40
```

---

# Simple Program

```cpp
#include <iostream>
using namespace std;

int main()
{
    int arr[5] = {10,20,30,40,50};

    cout << arr[0] << endl;
    cout << arr[1] << endl;
    cout << arr[2] << endl;

    return 0;
}
```

Output:

```text
10
20
30
```

---

# Accessing Array Using Loop

Manually:

```cpp
cout << arr[0];
cout << arr[1];
cout << arr[2];
cout << arr[3];
cout << arr[4];
```

Not scalable.

---

Using Loop:

```cpp
#include <iostream>
using namespace std;

int main()
{
    int arr[5] = {10,20,30,40,50};

    for(int i=0; i<5; i++)
    {
        cout << arr[i] << " ";
    }

    return 0;
}
```

Output:

```text
10 20 30 40 50
```

---

# How Loop Traverses Array?

Iteration 1:

```cpp
i = 0
```

Access:

```cpp
arr[0]
```

Output:

```text
10
```

---

Iteration 2:

```cpp
i = 1
```

Access:

```cpp
arr[1]
```

Output:

```text
20
```

---

Iteration 3:

```cpp
i = 2
```

Access:

```cpp
arr[2]
```

Output:

```text
30
```

And so on...

---

# Modifying Array Elements

Array ke kisi bhi element ko uske index ki help se modify kar sakte hain.

Example:

```cpp
int arr[5] = {10,20,30,40,50};
```

Modify:

```cpp
arr[2] = 100;
```

---

Before:

```text
Index     Value

0         10
1         20
2         30
3         40
4         50
```

After:

```text
Index     Value

0         10
1         20
2         100
3         40
4         50
```

---

# Complete Example

```cpp
#include <iostream>
using namespace std;

int main()
{
    int arr[5] = {10,20,30,40,50};

    arr[2] = 100;

    for(int i=0; i<5; i++)
    {
        cout << arr[i] << " ";
    }

    return 0;
}
```

Output:

```text
10 20 100 40 50
```

---