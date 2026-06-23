# Arrays Continued: Length, Traversal, For-Each Loop & Taking Input

---

# Finding Length of an Array

Suppose we have:

```cpp
int arr[] = {10, 20, 30, 40, 50};
```

Notice:

```cpp
[]
```

Size explicitly nahi diya gaya.

Compiler automatically calculate kar leta hai.

Lekin question hai:

```text
Length kaise nikale?
```

---

# Problem

C++ arrays ke paas JavaScript jaisa:

```cpp
arr.length
```

nahi hota.

Ye invalid hai.

```cpp
cout << arr.length;
```

❌ Error

---

# Formula for Length

C++ mein array length nikalne ka traditional formula:

```cpp
sizeof(arr) / sizeof(arr[0])
```

---

# Why Does This Work?

Example:

```cpp
int arr[] = {10,20,30,40,50};
```

Assume:

```text
int = 4 bytes
```

Array has:

```text
5 elements
```

Total memory:

```text
5 × 4

= 20 bytes
```

Therefore:

```cpp
sizeof(arr)
```

returns:

```text
20
```

---

First element:

```cpp
sizeof(arr[0])
```

returns:

```text
4
```

---

Formula:

```cpp
20 / 4

= 5
```

Length found.

---

# Example

```cpp
#include <iostream>
using namespace std;

int main()
{
    int arr[] = {10,20,30,40,50};

    int length =
        sizeof(arr) / sizeof(arr[0]);

    cout << length;

    return 0;
}
```

Output:

```text
5
```

---

# Traversing Array Using While Loop

Exactly same logic.

Only syntax changes in For loop.

```cpp
#include <iostream>
using namespace std;

int main()
{
    int arr[] = {10,20,30,40,50};

    int length =
        sizeof(arr) / sizeof(arr[0]);

    int i = 0;

    while(i < length)
    {
        cout << arr[i] << " ";

        i++;
    }

    return 0;
}
```

Output:

```text
10 20 30 40 50
```

---

# For Loop vs While Loop

For Loop:

```cpp
for(int i=0; i<length; i++)
```

Everything written in one place.

---

While Loop:

```cpp
int i = 0;

while(i < length)
{
    i++;
}
```

Initialization, condition, increment separate.

---

# Range Based For Loop (For-Each Loop)

Modern C++ introduced:

```cpp
for-each loop
```

Syntax:

```cpp
for(datatype variable : array)
{
}
```

Example:

```cpp
int marks[] = {80,85,90,95};
```

```cpp
for(int mark : marks)
{
    cout << mark << " ";
}
```

Output:

```text
80 85 90 95
```

---

# How It Works?

Internally:

```text
mark
```

takes value of each element one by one.

Iteration 1:

```text
mark = 80
```

Iteration 2:

```text
mark = 85
```

Iteration 3:

```text
mark = 90
```

Iteration 4:

```text
mark = 95
```

---

# Biggest Advantage

No need for:

```cpp
length
```

No need for:

```cpp
index
```

No risk of:

```text
Array Out of Bounds
```

---

# Taking Input Using Array

Example:

Store vowels.

```cpp
char vowels[5];
```

Input:

```text
a e i o u
```

---

# Input Using Normal For Loop

```cpp
#include <iostream>
using namespace std;

int main()
{
    char vowels[5];

    for(int i=0; i<5; i++)
    {
        cin >> vowels[i];
    }

    for(char vowel : vowels)
    {
        cout << vowel << " ";
    }

    return 0;
}
```

Output:

```text
a e i o u
```

---

# Common Beginner Doubt

Can we directly do this?

```cpp
for(char vowel : vowels)
{
    cin >> vowel;
}
```

Looks correct.

But actually:

```text
It does NOT work as intended.
```

---

# Why Doesn't It Work?

Very Important Concept.

Remember:

```cpp
for(char vowel : vowels)
```

creates:

```text
A COPY of every element.
```

Exactly like:

```text
Pass By Value
```

---

Visual

Suppose:

```cpp
vowels
```

contains:

```text
_ _ _ _ _
```

Iteration 1:

```cpp
char vowel = vowels[0];
```

COPY created.

User enters:

```text
a
```

Now:

```cpp
vowel = 'a'
```

But:

```cpp
vowels[0]
```

remains unchanged.

---

After loop ends:

```text
Copies destroyed
```

Original array:

```text
_ _ _ _ _
```

still unchanged.

---

# Solution: Use Reference

Instead:

```cpp
for(char &vowel : vowels)
{
    cin >> vowel;
}
```

Notice:

```cpp
&
```

Reference.

---

Now:

```text
vowel
```

is NOT a copy.

It becomes an alias of actual array element.

---

Visual

Iteration 1:

```cpp
vowel
```

directly refers to:

```cpp
vowels[0]
```

User enters:

```text
a
```

Now:

```cpp
vowels[0]
```

becomes:

```text
a
```

directly.

---

# Complete Program

```cpp
#include <iostream>
using namespace std;

int main()
{
    char vowels[5];

    cout << "Enter 5 vowels: ";

    for(char &vowel : vowels)
    {
        cin >> vowel;
    }

    cout << "Stored vowels: ";

    for(char vowel : vowels)
    {
        cout << vowel << " ";
    }

    return 0;
}
```

Output:

```text
Enter 5 vowels:
a e i o u

Stored vowels:
a e i o u
```

---

# Important Observation

Printing:

```cpp
for(char vowel : vowels)
```

is fine.

Because:

```text
We are only reading values.
```

---

Input:

```cpp
for(char vowel : vowels)
```

is wrong.

Because:

```text
We want to MODIFY values.
```

For modification:

```cpp
for(char &vowel : vowels)
```

must be used.

---

# Example Problem

Take N numbers from user and print their sum.

---

# Step 1

Take size from user.

```cpp
int n;
cin >> n;
```

---

# Step 2

Create array.

```cpp
int arr[n];
```

(We'll use this for learning purposes.)

---

# Step 3

Take input.

```cpp
for(int i=0; i<n; i++)
{
    cin >> arr[i];
}
```

---

# Step 4

Calculate sum.

```cpp
int sum = 0;

for(int num : arr)
{
    sum += num;
}
```

---

# Complete Program

```cpp
#include <iostream>
using namespace std;

int main()
{
    int n;

    cout << "How many numbers? ";
    cin >> n;

    int arr[n];

    cout << "Enter numbers: ";

    for(int i=0; i<n; i++)
    {
        cin >> arr[i];
    }

    int sum = 0;

    for(int num : arr)
    {
        sum += num;
    }

    cout << "Sum = "
         << sum;

    return 0;
}
```

---
