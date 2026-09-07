# Product of Array Except Self

## Problem ko samjho
Problem: https://leetcode.com/problems/product-of-array-except-self/description/

Suppose:

```text
nums = [1, 2, 3, 4]
```

Hume ek output array banana hai jisme har index `i` par poore array ke sabhi elements ka product ho, **except `nums[i]`**.

So:

```text
index 0 → 2 × 3 × 4 = 24
index 1 → 1 × 3 × 4 = 12
index 2 → 1 × 2 × 4 = 8
index 3 → 1 × 2 × 3 = 6
```

Output:

```text
[24, 12, 8, 6]
```

Normally hum total product ko current element se divide kar sakte the:

```text
1 × 2 × 3 × 4 = 24

24 / 1 = 24
24 / 2 = 12
24 / 3 = 8
24 / 4 = 6
```

But division allowed nahi hai.

Toh hume multiplication se solution banana hai.

---

# 1. Brute Force Approach

Sabse pehle simple solution socho.

Har index ke liye:

> "Main poore array mein jaunga aur current element ko chhodkar sabko multiply kar dunga."

Example:

```text
nums = [1, 2, 3, 4]
```

Index `0`:

```text
2 × 3 × 4 = 24
```

Index `1`:

```text
1 × 3 × 4 = 12
```

And so on.

Iske liye naturally two loops lagenge:

```cpp
for (int i = 0; i < n; i++) {

    int product = 1;

    for (int j = 0; j < n; j++) {

        if (i != j) {
            product *= nums[j];
        }
    }

    answer[i] = product;
}
```

### Complexity

Outer loop:

```text
O(n)
```

Inner loop:

```text
O(n)
```

Therefore:

```text
Time = O(n²)
```

Large `n` par ye TLE de sakta hai.

Ab important question:

> **Har index ke liye poora array dobara traverse karna zaroori hai kya?**

---

# 2. Answer Ko Left Aur Right Mein Tod Do

Example:

```text
nums = [1, 2, 3, 4]
```

Index `2` par current element `3` hai.

Hume chahiye:

```text
1 × 2 × 4
```

Ab isko split karo:

```text
left side  = 1 × 2 = 2
right side = 4
```

Therefore:

```text
answer[2] = 2 × 4
          = 8
```

Yaani har index ke liye:

```text
answer[i]
=
product of everything on the left
×
product of everything on the right
```

Yehi main observation hai.

---

# 3. Prefix Product

Left side ke product ko prefix product bol sakte hain.

For:

```text
nums = [1, 2, 3, 4]
```

Har index par left-side product:

```text
index 0 → nothing → 1
index 1 → 1       → 1
index 2 → 1×2     → 2
index 3 → 1×2×3   → 6
```

So:

```text
prefix = [1, 1, 2, 6]
```

`1` kyun?

Index ke left mein agar kuch nahi hai, toh product ko `1` rakhte hain because:

```text
1 × x = x
```

---

# 4. Suffix Product

Right side ke product ko suffix product bol sakte hain.

```text
nums = [1, 2, 3, 4]
```

Har index par right-side product:

```text
index 0 → 2×3×4 → 24
index 1 → 3×4   → 12
index 2 → 4     → 4
index 3 → nothing → 1
```

So:

```text
suffix = [24, 12, 4, 1]
```

---

# 5. Prefix × Suffix

Ab answer simply:

```text
answer[i] = prefix[i] × suffix[i]
```

So:

```text
index 0:
1 × 24 = 24

index 1:
1 × 12 = 12

index 2:
2 × 4 = 8

index 3:
6 × 1 = 6
```

Final:

```text
[24, 12, 8, 6]
```

Ab humne brute force ka repeated work eliminate kar diya.

---

# 6. Intermediate Solution — Prefix Aur Suffix Vectors

Ab is approach ko actual code mein implement karte hain.

Hum do arrays banayenge:

```text
prefix
suffix
```

Aur output:

```text
answer
```

### Step 1 — Prefix vector

```cpp
vector<int> prefix(n, 1);

int product = 1;

for (int i = 0; i < n; i++) {

    prefix[i] = product;

    product *= nums[i];
}
```

For:

```text
nums = [1, 2, 3, 4]
```

we get:

```text
prefix = [1, 1, 2, 6]
```

---

### Step 2 — Suffix vector

Ab right se left jaana hai.

```cpp
vector<int> suffix(n, 1);

int product = 1;

for (int i = n - 1; i >= 0; i--) {

    suffix[i] = product;

    product *= nums[i];
}
```

Result:

```text
suffix = [24, 12, 4, 1]
```

---

### Step 3 — Answer

Ab dono ko multiply kar do:

```cpp
for (int i = 0; i < n; i++) {

    answer[i] = prefix[i] * suffix[i];
}
```

Complete intermediate solution:

```cpp
class Solution {
public:
    vector<int> productExceptSelf(vector<int>& nums) {

        int n = nums.size();

        vector<int> prefix(n, 1);
        vector<int> suffix(n, 1);
        vector<int> answer(n);

        int product = 1;

        // Prefix products
        for (int i = 0; i < n; i++) {

            prefix[i] = product;

            product *= nums[i];
        }

        product = 1;

        // Suffix products
        for (int i = n - 1; i >= 0; i--) {

            suffix[i] = product;

            product *= nums[i];
        }

        // Prefix × Suffix
        for (int i = 0; i < n; i++) {

            answer[i] = prefix[i] * suffix[i];
        }

        return answer;
    }
};
```

---

# 7. Is Solution Ki Complexity

Humne three linear passes kiye:

```text
Prefix → O(n)
Suffix → O(n)
Answer → O(n)
```

So:

```text
O(n) + O(n) + O(n)
= O(n)
```

Time complexity excellent hai.

But space:

```text
prefix → O(n)
suffix → O(n)
answer → O(n)
```

Output array required hai, but `prefix` aur `suffix` extra hain.

So extra space is:

```text
O(n)
```

Ab next question:

> **Kya prefix aur suffix ke complete vectors store karna actually necessary hai?**

---

# 8. Prefix Vector Ko Remove Karna

Prefix vector:

```text
[1, 1, 2, 6]
```

ko dekho.

Ye values left-to-right gradually build ho rahi hain.

```text
prefix = 1

next:
1 × nums[0]

next:
previousPrefix × nums[1]

next:
previousPrefix × nums[2]
```

Matlab hume poora prefix vector calculate karke store karne ki zarurat nahi.

Sirf ek variable enough hai:

```cpp
int prefix = 1;
```

Lekin prefix information baad mein chahiye hogi.

Toh separate prefix vector banane ke bajaye:

> **Prefix products ko directly answer array mein store kar do.**

Example:

```text
nums = [1, 2, 3, 4]
```

Start:

```text
answer = [1, 1, 1, 1]
prefix = 1
```

Forward traversal:

```text
i = 0

answer[0] = 1
prefix = 1 × 1 = 1
```

```text
i = 1

answer[1] = 1
prefix = 1 × 2 = 2
```

```text
i = 2

answer[2] = 2
prefix = 2 × 3 = 6
```

```text
i = 3

answer[3] = 6
```

Now:

```text
answer = [1, 1, 2, 6]
```

Answer array temporarily prefix array ka kaam kar raha hai.

Separate prefix vector ki need khatam.

---

# 9. Suffix Vector Ko Remove Karna

Exactly same idea suffix ke saath.

Hume:

```text
suffix = [24, 12, 4, 1]
```

store karne ki zarurat nahi.

Ek variable enough hai:

```cpp
int suffix = 1;
```

Kyuki suffix right-to-left gradually build hota hai.

Reverse traversal:

```text
i = n - 1 → 0
```

Har index par:

```cpp
answer[i] *= suffix;
```

Then current element ko suffix mein add karo:

```cpp
suffix *= nums[i];
```

Important order:

```text
1. Existing suffix ko answer mein use karo
2. Uske baad current element ko suffix mein add karo
```

Why?

Because current element ko apne hi answer mein include nahi karna hai.

---

# 10. Final Space-Optimized Dry Run

Input:

```text
nums = [1, 2, 3, 4]
```

## Forward Pass

Start:

```text
answer = [1, 1, 1, 1]
prefix = 1
```

### i = 0

```text
answer[0] = prefix
           = 1
```

Then:

```text
prefix = 1 × 1
       = 1
```

### i = 1

```text
answer[1] = 1
```

Then:

```text
prefix = 1 × 2
       = 2
```

### i = 2

```text
answer[2] = 2
```

Then:

```text
prefix = 2 × 3
       = 6
```

### i = 3

```text
answer[3] = 6
```

Now:

```text
answer = [1, 1, 2, 6]
```

Ye prefix products hain.

---

## Backward Pass

Start:

```text
suffix = 1
```

### i = 3

```text
answer[3] = 6 × 1
          = 6
```

Then:

```text
suffix = 1 × 4
       = 4
```

### i = 2

```text
answer[2] = 2 × 4
          = 8
```

Then:

```text
suffix = 4 × 3
       = 12
```

### i = 1

```text
answer[1] = 1 × 12
          = 12
```

Then:

```text
suffix = 12 × 2
       = 24
```

### i = 0

```text
answer[0] = 1 × 24
          = 24
```

Final:

```text
answer = [24, 12, 8, 6]
```

---

# 11. Zero Wala Case

Example:

```text
nums = [1, 2, 0, 4]
```

Expected:

```text
[0, 0, 8, 0]
```

Index `2` par zero ko exclude karna hai:

```text
1 × 2 × 4 = 8
```

Baaki indexes ke products mein zero included hai, so unka answer `0`.

Prefix-suffix approach mein zero ke liye koi special condition nahi likhni padti.

Normal multiplication automatically handle kar leti hai.

---

# 12. Negative Numbers

Negative values bhi normally work karti hain.

Example:

```text
nums = [-1, 2, 3, 4]
```

Prefix aur suffix products normal multiplication se calculate honge.

Koi separate negative-number logic required nahi hai.

---

# 13. Final Code

```cpp
class Solution {
public:
    vector<int> productExceptSelf(vector<int>& nums) {

        int n = nums.size();

        vector<int> answer(n, 1);

        int prefix = 1;

        // Store prefix products in answer
        for (int i = 0; i < n; i++) {

            answer[i] = prefix;

            prefix *= nums[i];
        }

        int suffix = 1;

        // Multiply suffix products into answer
        for (int i = n - 1; i >= 0; i--) {

            answer[i] *= suffix;

            suffix *= nums[i];
        }

        return answer;
    }
};
```

---

# 14. Complexity

Time:

```text
O(n)
```

Space:

```text
O(1) extra space
```

`answer` output array hai, jo required hai.

Extra mein sirf:

```text
prefix
suffix
```

variables hain.

Isliye prefix/suffix vectors remove karne ke baad extra space `O(1)` ho jaati hai.
