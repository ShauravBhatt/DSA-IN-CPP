# Vectors in C++ - Fundamentals

# What is a Vector?

Vector is a **dynamic array** provided by the C++ STL (Standard Template Library).

Think of it like:

```text
Array  → Fixed Size

Vector → Dynamic Size
```

With arrays:

```cpp
int arr[5];
```

Size is fixed.

Once created:

```text
Cannot grow automatically.
```

---

With vectors:

```cpp
vector<int> nums;
```

Size can increase or decrease during runtime.

This is the biggest advantage of vectors.

---

# Header File

To use vectors:

```cpp
#include <vector>
```

---

# What Type of Data Can Vectors Store?

Vector can store any data type.

### Integer Vector

```cpp
vector<int> nums;
```

---

### Character Vector

```cpp
vector<char> letters;
```

---

### Double Vector

```cpp
vector<double> prices;
```

---

### String Vector

```cpp
vector<string> names;
```

---

# Vector Syntax

General Syntax:

```cpp
vector<dataType> vectorName;
```

Example:

```cpp
vector<int> marks;
```

Meaning:

```text
Vector Name : marks

Data Type   : int
```

---

# Different Ways to Initialize Vectors

# 1. Initializer List

Direct values provide karte hain.

```cpp
vector<int> nums = {10,20,30,40,50};
```

Memory:

```text
10 20 30 40 50
```

---

# 2. Uniform Initialization

Modern C++ style.

```cpp
vector<int> nums{10,20,30,40,50};
```

Same result.

Many modern codebases prefer this style.

---

# 3. Specify Size and Default Value

Syntax:

```cpp
vector<int> nums(size, value);
```

Example:

```cpp
vector<int> nums(5, 100);
```

Meaning:

```text
Create 5 elements

Each element = 100
```

Result:

```text
100 100 100 100 100
```

---

Another Example:

```cpp
vector<int> nums(4, 0);
```

Result:

```text
0 0 0 0
```

---

# Size of a Vector

Size means:

```text
Currently kitne elements vector ke andar hain.
```

Example:

```cpp
vector<int> nums = {10,20,30};
```

Size:

```cpp
nums.size()
```

Output:

```text
3
```

---

# Capacity of a Vector

Capacity means:

```text
Vector ne internally kitni storage reserve kar rakhi hai.
```

Example:

```cpp
vector<int> nums = {10,20,30};
```

```cpp
nums.capacity()
```

Could be:

```text
4
```

or

```text
8
```

depending on compiler implementation.

---

# Important Rule

```text
Capacity ≥ Size
```

Always.

---

Possible:

```text
Size = 3

Capacity = 4
```

---

Possible:

```text
Size = 5

Capacity = 8
```

---

Impossible:

```text
Size = 8

Capacity = 5
```

❌

Because capacity can never be smaller than size.

---

# Checking Size and Capacity

Example:

```cpp
#include <iostream>
#include <vector>
using namespace std;

int main()
{
    vector<int> nums = {10,20,30};

    cout << nums.size() << endl;

    cout << nums.capacity();

    return 0;
}
```

---

# Accessing Elements

Exactly same as arrays.

Example:

```cpp
vector<int> nums = {10,20,30,40,50};
```

Access:

```cpp
cout << nums[0];
```

Output:

```text
10
```

---

```cpp
cout << nums[3];
```

Output:

```text
40
```

---

# Traversing a Vector

Using For Loop:

```cpp
for(int i=0; i<nums.size(); i++)
{
    cout << nums[i] << " ";
}
```

---

Using For-Each Loop:

```cpp
for(int num : nums)
{
    cout << num << " ";
}
```

---

# Resizing a Vector

Suppose:

```cpp
vector<int> nums = {10,20,30};
```

Size:

```text
3
```

---

Resize:

```cpp
nums.resize(5);
```

Now:

```text
10 20 30 0 0
```

Size becomes:

```text
5
```

---

Example:

```cpp
nums.resize(7,100);
```

Result:

```text
10 20 30 0 0 100 100
```

New elements initialized with:

```text
100
```

---

# How Vector Works Internally?

This is where vectors become interesting.

Suppose:

```cpp
vector<int> nums;
```

Initially:

```text
Size = 0

Capacity = 0
```

---

Push First Element

```cpp
nums.push_back(10);
```

Now:

```text
Size     = 1

Capacity = 1
```

---

Push Second Element

```cpp
nums.push_back(20);
```

Now:

```text
Size     = 2

Capacity = 2
```

---

Push Third Element

```cpp
nums.push_back(30);
```

Current capacity:

```text
2
```

But we need space for:

```text
3 elements
```

No space available.

---

Vector does something smart.

It allocates a bigger memory block.

Usually:

```text
Old Capacity = 2

New Capacity = 4
```

Then:

```text
Copies old elements

Deletes old memory

Uses new memory
```

Now:

```text
Size     = 3

Capacity = 4
```

---

Push Fourth Element

```cpp
nums.push_back(40);
```

Now:

```text
Size     = 4

Capacity = 4
```

Still okay.

---

Push Fifth Element

```cpp
nums.push_back(50);
```

Again capacity full.

Vector reallocates.

Often:

```text
Old Capacity = 4

New Capacity = 8
```

Now:

```text
Size     = 5

Capacity = 8
```

---

# Visualization

```text
Size = 1
Capacity = 1

[10]
```

---

```text
Size = 2
Capacity = 2

[10][20]
```

---

```text
Size = 3
Capacity = 4

[10][20][30][ ]
```

---

```text
Size = 5
Capacity = 8

[10][20][30][40][50][ ][ ][ ]
```

---

# Does Capacity Always Double?

Most implementations:

```text
Usually increase exponentially.
```

Often:

```text
1 → 2 → 4 → 8 → 16 → 32
```

But:

```text
This is implementation dependent.
```

Different compilers may grow differently.

---

The important thing to remember is:

```text
Capacity grows faster than Size.
```

So vector doesn't need to reallocate memory every single insertion.

This makes:

```cpp
push_back()
```

extremely efficient in practice.

---

# Why Vectors Are Preferred in DSA?

Because they provide:

```text
✓ Dynamic Size

✓ Automatic Memory Management

✓ Easy Insertions

✓ STL Support

✓ Cleaner Code
```

And that's why almost every beginner and intermediate DSA problem nowadays starts with:

```cpp
vector<int> nums;
```

instead of:

```cpp
int arr[1000];
```