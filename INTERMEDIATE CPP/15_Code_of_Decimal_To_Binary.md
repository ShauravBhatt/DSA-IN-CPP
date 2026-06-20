# Binary Conversion Using Code & Bit Manipulation Notes

# 1. The Core Insight

Jab hum manually decimal to binary convert karte hain:

```text
13 ÷ 2 = 6 remainder 1
6 ÷ 2 = 3 remainder 0
3 ÷ 2 = 1 remainder 1
1 ÷ 2 = 0 remainder 1
```

Hum actually do kaam kar rahe hote hain:

```text
1. Last Bit nikal rahe hain
2. Last Bit hata rahe hain
```

Aur computer bhi exactly yahi karta hai.

Isliye Bit Manipulation ka foundation hai:

```cpp
n & 1
n >> 1
```

---

# 2. Why n & 1 Works?

Suppose:

```cpp
n = 13
```

Binary:

```text
1101
```

Ab:

```cpp
n & 1
```

Actually:

```text
1101
0001
----
0001
```

Result:

```text
1
```

---

# What is it Checking?

Sirf last bit.

```text
Last Bit = 1
```

Matlab:

```text
Odd Number
```

---

Example:

```cpp
n = 10
```

Binary:

```text
1010
```

```text
1010
0001
----
0000
```

Result:

```text
0
```

Last bit:

```text
0
```

Matlab:

```text
Even Number
```

---

# Odd-Even Rule

```cpp
if(n & 1)
```

Means:

```text
Odd
```

---

```cpp
if((n & 1) == 0)
```

Means:

```text
Even
```

---

# Why Does This Work?

Remember:

```text
Odd Number = remainder 1 when divided by 2
Even Number = remainder 0 when divided by 2
```

And:

```cpp
n & 1
```

gives exactly:

```text
n % 2
```

for positive integers.

---

# Quick Examples

```cpp
5 = 101
```

```cpp
5 & 1
```

```text
101
001
---
001
```

Result:

```text
1
```

Odd.

---

```cpp
8 = 1000
```

```text
1000
0001
----
0000
```

Result:

```text
0
```

Even.

---

# 3. Why n >> 1 Works?

Suppose:

```cpp
n = 13
```

Binary:

```text
1101
```

---

Right Shift:

```cpp
n >> 1
```

Result:

```text
110
```

Decimal:

```text
6
```

---

Check:

```text
13 / 2 = 6
```

Same answer.

---

Another Example

```cpp
8 = 1000
```

Shift:

```text
1000
↓
0100
```

Decimal:

```text
4
```

And:

```text
8 / 2 = 4
```

---

# Intuition

Right Shift means:

```text
Remove Last Bit
```

And mathematically:

```cpp
n >> 1
```

acts like:

```cpp
n / 2
```

(integer division)

---

# 4. How Computer Extracts Binary

Take:

```cpp
n = 13
```

Binary:

```text
1101
```

---

Iteration 1

```cpp
bit = n & 1
```

```text
1
```

Store:

```text
1
```

Now:

```cpp
n >>= 1
```

```text
1101 → 110
```

```cpp
n = 6
```

---

Iteration 2

```cpp
bit = n & 1
```

```text
0
```

Store:

```text
10
```

Shift:

```text
110 → 11
```

```cpp
n = 3
```

---

Iteration 3

```cpp
bit = 1
```

Store:

```text
101
```

Shift:

```cpp
n = 1
```

---

Iteration 4

```cpp
bit = 1
```

Store:

```text
1011
```

Shift:

```cpp
n = 0
```

Stop.

---

Bits Obtained:

```text
1 0 1 1
```

Notice:

```text
Reverse Order
```

---

# Why Reverse Order?

Computer always sees:

```text
LSB First
```

Meaning:

```text
Right Most Bit First
```

---

For:

```text
1101
```

Computer extracts:

```text
1
0
1
1
```

from right to left.

But binary is written:

```text
1
1
0
1
```

from left to right.

Therefore:

```text
Reverse Required
```

---

# 5. Formula Behind Binary Construction

Suppose extracted bits are:

```text
1
0
1
1
```

---

First Bit

```cpp
ans = 1
```

---

Second Bit

```cpp
ans = 0*10 + 1
```

```text
1
```

---

Third Bit

```cpp
ans = 1*100 + 1
```

```text
101
```

---

Fourth Bit

```cpp
ans = 1*1000 + 101
```

```text
1101
```

---

General Formula

```cpp
ans = bit * pow(10, i) + ans;
```

where:

```text
bit = current extracted bit
i   = current position
```

---

# 6. Decimal to Binary Code

## Method 1

```cpp
#include <iostream>
#include <cmath>
using namespace std;

int main()
{
    int n = 13;

    int ans = 0;
    int i = 0;

    while(n > 0)
    {
        int bit = n & 1;

        ans = (bit * pow(10, i)) + ans;

        n = n >> 1;

        i++;
    }

    cout << ans;
}
```

Output:

```text
1101
```

---

# Dry Run

Initial:

```cpp
n = 13
ans = 0
```

---

Loop 1

```cpp
bit = 1
```

```cpp
ans = 1
```

```cpp
n = 6
```

---

Loop 2

```cpp
bit = 0
```

```cpp
ans = 1
```

```cpp
n = 3
```

---

Loop 3

```cpp
bit = 1
```

```cpp
ans = 101
```

```cpp
n = 1
```

---

Loop 4

```cpp
bit = 1
```

```cpp
ans = 1101
```

```cpp
n = 0
```

Stop.