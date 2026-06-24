# Vectors in C++ - Insertion, Deletion & Input

# Adding Elements in a Vector

There are multiple ways to add elements in a vector.

---

# 1. push_back()

Most commonly used function.

Adds element at the end of vector.

Syntax:

```cpp
vectorName.push_back(value);
```

Example:

```cpp
vector<int> nums = {10,20,30};

nums.push_back(40);
```

Before:

```text
10 20 30
```

After:

```text
10 20 30 40
```

---

# Code

```cpp
#include <iostream>
#include <vector>
using namespace std;

int main()
{
    vector<int> nums = {10,20,30};

    nums.push_back(40);

    for(int num : nums)
    {
        cout << num << " ";
    }
}
```

Output:

```text
10 20 30 40
```

---

# 2. insert()

Used to insert element at any position.

Syntax:

```cpp
vectorName.insert(
    vectorName.begin() + index,
    value
);
```

---

Example

```cpp
vector<int> nums = {10,20,30,40};

nums.insert(nums.begin()+2, 100);
```

Before:

```text
10 20 30 40
```

After:

```text
10 20 100 30 40
```

---

Visualization

```text
Index

0 1 2 3

10 20 30 40
      ↑

Insert Here
```

After insertion:

```text
10 20 100 30 40
```

Remaining elements shift right.

---

# Code

```cpp
vector<int> nums = {10,20,30,40};

nums.insert(nums.begin()+2,100);
```

---

# What is begin()?

```cpp
nums.begin()
```

returns iterator to first element.

Think of it as:

```text
Starting position of vector.
```

---

Example:

```cpp
nums.begin()+0
```

First position

---

```cpp
nums.begin()+2
```

Third position

---

# push_front()

Many beginners expect:

```cpp
nums.push_front(10);
```

But:

```text
vector does NOT support push_front()
```

❌ Error

---

Reason:

Vector is optimized for:

```text
Insertion at end
```

not beginning.

---

If you need frequent insertion at front:

```cpp
deque
```

is generally preferred.

---

# Removing Elements

# 1. pop_back()

Removes last element.

Syntax:

```cpp
vectorName.pop_back();
```

Example:

```cpp
vector<int> nums = {10,20,30,40};

nums.pop_back();
```

Before:

```text
10 20 30 40
```

After:

```text
10 20 30
```

---

# Code

```cpp
vector<int> nums = {10,20,30,40};

nums.pop_back();
```

---

# pop_front()

Again:

```cpp
vector does NOT have pop_front()
```

❌

Because removing from front requires shifting all elements.

---

# erase()

Used to remove element from a specific position.

Syntax:

```cpp
vectorName.erase(
    vectorName.begin()+index
);
```

---

Example

```cpp
vector<int> nums =
{
    10,20,30,40,50
};

nums.erase(nums.begin()+2);
```

Before:

```text
10 20 30 40 50
```

After:

```text
10 20 40 50
```

---

Notice:

```text
30 removed

Remaining elements shifted left
```

---

# Code

```cpp
vector<int> nums =
{
    10,20,30,40,50
};

nums.erase(nums.begin()+2);
```

---

# Removing a Range

Example:

```cpp
nums.erase(
    nums.begin()+1,
    nums.begin()+4
);
```

Removes:

```text
Index 1

Index 2

Index 3
```

---

Example:

Before:

```text
10 20 30 40 50
```

After:

```text
10 50
```

---

# Taking Input in Vector

Suppose user wants:

```text
5 numbers
```

---

Create vector

```cpp
vector<int> nums(5);
```

---

Using For Loop

```cpp
for(int i=0; i<nums.size(); i++)
{
    cin >> nums[i];
}
```

---

# Taking Input Using For-Each Loop

Yes, possible.

But use Reference.

Correct:

```cpp
for(int &num : nums)
{
    cin >> num;
}
```

---

Why Reference?

Because:

```cpp
num
```

must directly modify vector element.

---

Wrong:

```cpp
for(int num : nums)
{
    cin >> num;
}
```

---

Reason:

```text
num becomes a COPY
```

Exactly same as:

```text
Pass By Value
```

Changes disappear after iteration.

---

Correct:

```cpp
for(int &num : nums)
{
    cin >> num;
}
```

Now:

```text
num becomes alias
of actual vector element.
```

---

# Complete Input Example

```cpp
#include <iostream>
#include <vector>
using namespace std;

int main()
{
    vector<int> nums(5);

    for(int &num : nums)
    {
        cin >> num;
    }

    for(int num : nums)
    {
        cout << num << " ";
    }
}
```

---

# Problem: Last Occurrence of an Element

Question:

Find last occurrence of:

```text
10
```

in:

```text
10 20 30 10 40 10
```

---

Expected Answer

```text
Index = 5
```

---

# Logic

Start from end.

Because:

```text
We need LAST occurrence.
```

---

Instead of:

```text
0 → n-1
```

go:

```text
n-1 → 0
```

---

Visualization

```text
10 20 30 10 40 10

             ↑

Start Here
```

---

As soon as value found:

```text
Return Index
```

---

# Code

```cpp
#include <iostream>
#include <vector>
using namespace std;

int main()
{
    vector<int> nums =
    {
        10,20,30,10,40,10
    };

    int target = 10;

    int index = -1;

    for(int i=nums.size()-1;
        i>=0;
        i--)
    {
        if(nums[i] == target)
        {
            index = i;
            break;
        }
    }

    cout << index;
}
```

Output:

```text
5
```

---

# Time Complexity

Loop may visit every element.

```text
O(n)
```

---

# Quick Understanding

### Insert at End

```cpp
push_back(value);
```

---

### Insert at Any Position

```cpp
insert(begin()+index,value);
```

---

### Remove Last Element

```cpp
pop_back();
```

---

### Remove By Position

```cpp
erase(begin()+index);
```

---

### Take Input

```cpp
for(int &x : nums)
{
    cin >> x;
}
```

---

### Find Last Occurrence

```cpp
Traverse from right to left.
```

Because:

```text
Last occurrence is closer to end.
```
