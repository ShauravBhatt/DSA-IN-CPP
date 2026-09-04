# Binary Exponentiation — Pow(x, n)

## 1. Problem
Leetcode Link: https://leetcode.com/problems/powx-n/description/

Hume calculate karna hai:

\[
x^n
\]

Example:

```text
2^10 = 1024
2^-2 = (1 / 2)^2 = 0.25
```

Important constraint:

```text
-2^31 <= n <= 2^31 - 1
```

Yani `n` bahut bada ho sakta hai.

---

## 2. Brute Force Approach

Sabse simple approach hai `x` ko `n` times multiply karna.

For example:

```text
3^5 = 3 × 3 × 3 × 3 × 3
```

Is approach ki time complexity:

```text
O(n)
```

Problem ye hai ki `n` approximately 2 billion tak ja sakta hai.

### `10^8` operations kya hota hai?

DSA/competitive programming mein roughly `10^8` simple operations ko ek practical upper range maana ja sakta hai. Ye exact rule nahi hai; actual runtime machine, language aur operation par depend karta hai.

```text
10^8       = 100 million
2^31       ≈ 2.1 billion
```

Toh `O(n)` solution worst case mein billions of iterations kar sakta hai, jiski wajah se **TLE** aa sakta hai.

Humein `O(n)` se better approach chahiye.

---

# 3. Optimization ka Main Idea

Ek important observation:

```text
3^8 = 3^4 × 3^4
3^4 = 3^2 × 3^2
3^2 = 3 × 3
```

Hum powers ko repeatedly **square** karke bana sakte hain:

```text
3^1
 ↓ square
3^2
 ↓ square
3^4
 ↓ square
3^8
 ↓ square
3^16
```

Exponent:

```text
1 → 2 → 4 → 8 → 16 → ...
```

Har step mein exponent double ho raha hai.

Isliye `n` times loop chalane ke bajay hum approximately `log₂(n)` times loop chala sakte hain.

So:

```text
Brute Force       → O(n)
Binary Exponent.  → O(log n)
```

---

# 4. Binary Representation ka Connection

Suppose:

```text
n = 13
```

Binary:

```text
13 = 1101
```

Iska meaning:

```text
13 = 8 + 4 + 1
```

Therefore:

```text
x^13
= x^(8+4+1)
= x^8 × x^4 × x^1
```

Ab humein sirf:

```text
x^1
x^4
x^8
```

chahiye.

Aur ye powers repeatedly squaring se mil jayengi:

```text
x^1 → x^2 → x^4 → x^8
```

Binary mein jahan `1` hai, corresponding power ko answer mein multiply karna hai.

```text
13 = 1101

1 → x^8   take
1 → x^4   take
0 → x^2   skip
1 → x^1   take
```

Yahi **Binary Exponentiation** ka main idea hai.

---

# 5. Binary Digits ko Directly Kaise Process Karein?

Humein binary representation ko explicitly store karne ki zarurat nahi hai.

### Last binary digit

```cpp
n % 2
```

batata hai ki last binary bit `0` hai ya `1`.

```text
even number → n % 2 = 0
odd number  → n % 2 = 1
```

### Next binary digit

```cpp
n /= 2;
```

se hum next bit par move karte hain.

Example:

```text
13 → 6 → 3 → 1 → 0
```

Binary mein:

```text
1101
 ↓
110
 ↓
11
 ↓
1
 ↓
0
```

So har iteration mein ek binary digit process ho rahi hai.

---

# 6. `x` ko Kaise Update Karenge?

Initially:

```text
x = x^1
```

Har iteration:

```cpp
x *= x;
```

So:

```text
x^1 → x^2 → x^4 → x^8 → x^16 → ...
```

Aur agar current binary digit `1` hai, current `x` answer mein include karenge.

---

# 7. Dry Run — `3^13`

Initial:

```text
x = 3
n = 13
answer = 1
```

### Iteration 1

```text
n = 13
13 % 2 = 1
```

Bit `1`, so current power `3^1` ko answer mein lo:

```text
answer = 1 × 3 = 3
```

Next power:

```text
x = 3 × 3 = 9 = 3^2
```

Next binary digit:

```text
n = 13 / 2 = 6
```

---

### Iteration 2

```text
n = 6
6 % 2 = 0
```

Bit `0`, so `3^2` ko skip karo.

```text
answer = 3
```

Next power:

```text
x = 9 × 9 = 81 = 3^4
```

Next:

```text
n = 6 / 2 = 3
```

---

### Iteration 3

```text
n = 3
3 % 2 = 1
```

Bit `1`, so `3^4` lo:

```text
answer = 3 × 81 = 243
```

Next power:

```text
x = 81 × 81 = 6561 = 3^8
```

Next:

```text
n = 3 / 2 = 1
```

---

### Iteration 4

```text
n = 1
1 % 2 = 1
```

Bit `1`, so `3^8` lo:

```text
answer = 243 × 6561
       = 1594323
```

Then:

```text
n = 1 / 2 = 0
```

Loop ends.

Final:

```text
3^13 = 1594323
```

Notice selected powers:

```text
3^1 × 3^4 × 3^8
```

which exactly matches:

```text
13 = 1 + 4 + 8
```

---

# 8. Negative Exponent

LeetCode mein `n` negative bhi ho sakta hai.

Example:

```text
2^-3
```

Mathematical rule:

\[
x^{-n} = \frac{1}{x^n}
\]

Therefore:

```text
2^-3
= (1/2)^3
= 0.125
```

So agar:

```text
n < 0
```

toh:

```text
x = 1 / x
n = -n
```

Example:

```text
x = 2
n = -3
```

becomes:

```text
x = 1/2
n = 3
```

Ab same Binary Exponentiation algorithm chalega.

### Important C++ detail

`n` ko directly `int` ke andar negate karna problematic ho sakta hai for:

```text
n = -2^31
```

because positive `2^31` signed 32-bit `int` mein fit nahi hota.

Isliye:

```cpp
long long N = n;
```

use karna safer hai.

---

# 9. Corner Cases

## Case 1: `n = 0`

Mathematical rule:

```text
x^0 = 1
```

Examples:

```text
5^0 = 1
-3^0 = 1
```

Algorithm mein bhi `N = 0` hone par loop chalega hi nahi, aur `answer` initially `1.0` hai.

---

## Case 2: `n = 1`

```text
x^1 = x
```

Example:

```text
5^1 = 5
```

Algorithm naturally handle karta hai.

---

## Case 3: Negative `n`

```text
2^-2 = 1/4 = 0.25
```

Isliye negative exponent ko reciprocal mein convert karna hai.

---

## Case 4: `x = 1`

```text
1^n = 1
```

Positive aur negative exponent dono mein answer `1` rahega.

---

## Case 5: `x = -1`

Pattern:

```text
(-1)^1 = -1
(-1)^2 = 1
(-1)^3 = -1
(-1)^4 = 1
```

So:

```text
odd exponent  → -1
even exponent → 1
```

Binary Exponentiation ise bhi naturally handle kar leta hai.

---

## Case 6: `x = 0`

For positive exponent:

```text
0^n = 0
```

Example:

```text
0^5 = 0
```

`0^0` ko blindly handle nahi karna chahiye; problem ke given constraints/convention ko follow karna chahiye.

---

# 10. Final Code

```cpp
class Solution {
public:
    double myPow(double x, int n) {

        long long N = n;

        if (N < 0) {
            x = 1 / x;
            N = -N;
        }

        double ans = 1.0;

        while (N > 0) {

            if (N % 2 == 1) {
                ans *= x;
            }

            x *= x;
            N /= 2;
        }

        return ans;
    }
};
```

---

# 11. Complexity

Every iteration mein:

```text
N → N / 2
```

So number of iterations:

```text
O(log n)
```

Therefore:

```text
Time Complexity  = O(log n)
Space Complexity = O(1)
```

The main optimization is simply:

```text
O(n)
   ↓
Use binary representation of n
   ↓
Repeatedly square x
   ↓
Divide n by 2 every iteration
   ↓
O(log n)
```
