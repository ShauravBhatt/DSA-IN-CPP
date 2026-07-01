# Pair Sum (Sorted Array) — Brute Force → Two Pointer

## Problem

Given a **sorted array** and a target, find the indices of two numbers whose sum is equal to the target.

Example:

```cpp
arr = {2, 7, 11, 15}

target = 13
```

Required Answer

```text
Index 0 and Index 2

Because,

2 + 11 = 13
```

---

# Approach 1 : Brute Force

Whenever we solve a new problem, the first question should always be

> **"Agar mujhe koi optimization nahi aati, to main is problem ko kaise solve karunga?"**

Sabse obvious answer hai,

> **Har possible pair check kar lo.**

Isi thinking ko code mein likha gaya hai.

```cpp
for (int start = 0; start < arr.size(); start++)
{
    for (int end = start + 1; end < arr.size(); end++)
    {
        if (target == arr[start] + arr[end])
        {
            ans.push_back(start);
            ans.push_back(end);
            break;
        }
    }
}
```

Ab is code ko line by line samajhte hain.

---

## Step 1 : First Number Kaun Hoga?

```cpp
for (int start = 0; start < arr.size(); start++)
```

Ye loop first number choose karta hai.

Initially

```text
start = 0
```

To first number hai

```text
2
```

Uske baad

```text
start = 1
```

To first number ban gaya

```text
7
```

Aur aise hi har element ek baar first number banega.

---

## Step 2 : Second Number Kaun Hoga?

Ab question aata hai.

> **Pehla number mil gaya. Ab uske saath kis-kis ko check karna hai?**

Uske liye second loop.

```cpp
for (int end = start + 1; end < arr.size(); end++)
```

Dhyan do.

Ye `start + 1` se shuru ho raha hai.

`start` se nahi.

Kyun?

Kyuki ek element ko khud ke saath pair nahi bana sakte.

Example

Agar

```text
start = 0
```

To pairs banenge

```text
(2,7)

(2,11)

(2,15)
```

Lekin

```text
(2,2)
```

kabhi check nahi hoga.

Isi liye `start + 1`.

---

## Step 3 : Pair Target Ke Equal Hai?

Har iteration mein ye line chalti hai.

```cpp
if(target == arr[start] + arr[end])
```

Suppose

```text
2 + 7 = 9
```

Target

```text
13
```

Equal nahi hai.

To next pair.

```text
2 + 11 = 13
```

Equal mil gaya.

Ab answer mil chuka hai.

To indices store kar do.

```cpp
ans.push_back(start);

ans.push_back(end);
```

Aur

```cpp
break;
```

kyuki is starting index ke liye answer mil gaya.

---

## Dry Run (Brute Force)

```text
Array

2   7   11   15

Target = 13
```

Pairs checked

```text
2 + 7 = 9 ❌

2 + 11 = 13 ✅
```

Answer

```text
0 2
```

Ye approach bilkul sahi hai.

Lekin ek question.

> **Kya hume sach mein har pair check karna zaroori hai?**

Yahin se optimization shuru hoti hai.

---

# Observation

Array ko dhyan se dekho.

```text
2   7   11   15
```

Ye random nahi hai.

Ye already **sorted** hai.

Ab ek question.

> **Agar array sorted hai, to kya hume uska koi advantage mil sakta hai?**

Bilkul.

Isi observation se **Two Pointer Technique** aati hai.

---

# Two Pointer Technique

Instead of checking every pair,

hum sirf do pointers rakhenge.

```text
L                 R

2   7   11   15
```

Ek pointer beginning par.

Ek pointer end par.

Ab har step par hum sirf ek question poochte hain.

> **Current pair ka sum target se chhota hai, bada hai, ya equal hai?**

Usi answer ke basis par pointer move karte hain.

---

## Case 1 : Sum Target Se Chhota Hai

Suppose

```text
Array

2   7   11   15

Target = 20
```

Current sum

```text
2 + 15 = 17
```

Question.

> **17 ko 20 banana hai. Sum badhana hai ya ghatana hai?**

Clearly,

sum badhana hai.

Ab socho.

Array sorted hai.

Right pointer already sabse bada element pakad ke baitha hai.

Agar right ko left laoge,

```text
15

↓

11
```

Sum aur chhota ho jayega.

Ye to opposite direction hai.

To sirf ek option bachta hai.

```text
Left Pointer ko aage badhao.
```

Kyuki left aage jayega.

```text
2

↓

7
```

Number bada hoga.

Aur sum bhi bada hoga.

Isliye rule ban gaya.

```text
Current Sum < Target

↓

Move Left Pointer
```

---

## Case 2 : Sum Target Se Bada Hai

Suppose

```text
Target = 13
```

Current pair

```text
2 + 15 = 17
```

Question.

> **17 ko 13 banana hai. Sum badhana hai ya ghatana hai?**

Sum ghatana hai.

Ab socho.

Agar left pointer aage badhega,

```text
2

↓

7
```

Sum banega

```text
7 + 15 = 22
```

Aur bada ho gaya.

Ye bhi galat direction hai.

To sirf ek option bachta hai.

```text
Right Pointer ko peeche lao.
```

Kyuki

```text
15

↓

11
```

Number chhota ho gaya.

Aur sum bhi chhota ho gaya.

Isliye second rule bana.

```text
Current Sum > Target

↓

Move Right Pointer
```

---

## Case 3 : Sum Target Ke Equal Hai

Agar

```text
Current Sum == Target
```

To answer mil gaya.

Indices return kar do.

---

# Applying Two Pointer to This Problem

Ab code dekhte hain.

```cpp
int left = 0;
int right = arr.size() - 1;
```

Initially

```text
L                 R

2   7   11   15
```

---

Loop tab tak chalega jab tak dono pointers mil nahi jaate.

```cpp
while(left < right)
```

Kyuki jab

```text
left == right
```

ho jayega,

to ek hi element bach gaya.

Usse pair nahi ban sakta.

---

Ab har iteration mein current sum check karte hain.

```cpp
arr[left] + arr[right]
```

Initially

```text
2 + 15 = 17
```

Target

```text
13
```

17 bada hai.

To kis pointer ko move karenge?

Right.

Isi liye

```cpp
right--;
```

Ab array dikhegi

```text
L             R

2   7   11   15
```

Current sum

```text
2 + 11 = 13
```

Target mil gaya.

Ab answer store kar do.

```cpp
ans.push_back(left);

ans.push_back(right);
```

Aur

```cpp
break;
```

Kyuki answer mil chuka hai.

---

# Complete Dry Run

```text
Array

2   7   11   15

Target = 13
```

| Left | Right | Pair   | Sum | Decision                                                  |
| ---- | ----- | ------ | --- | --------------------------------------------------------- |
| 0    | 3     | 2 + 15 | 17  | Sum is greater than target → Move Right to One index Left |
| 0    | 2     | 2 + 11 | 13  | Target Found ✅                                           |

Final Answer

```text
Indices = {0, 2}
```

---

### Final Solution

```cpp
    vector<int> arr = {2, 7, 11, 15};
    int target = 13;
    vector<int> ans;

    int left = 0;
    int right = arr.size() - 1;


    while (left < right)
    {
        if (arr[left] + arr[right] > target)
        {
            right--;
        }
        else if (arr[left] + arr[right] < target)
        {
            left++;
        }
        else
        {
            ans.push_back(left);
            ans.push_back(right);
            break;
        }
    }

    cout << "Indices are: \n";
    cout << ans[0] << ", " << ans[1] << "\n";
```

---

# Why is this Faster?

Brute Force mein

Har element ke saath almost har element compare ho raha tha.

```text
O(n²)
```

Two Pointer mein

Har iteration mein ya to

- Left aage badhta hai

ya

- Right peeche aata hai.

Dono pointers kabhi reverse direction mein nahi jaate.

Isliye maximum `n` movements hi honge.

Time Complexity

```text
O(n)
```

Space Complexity

```text
O(1)
```

---

# Important Note

Ye approach tabhi kaam karti hai jab **array sorted ho**.

Agar array sorted nahi hai aur original indices preserve karni hain (jaise original LeetCode Two Sum problem mein), to Two Pointer directly apply nahi hota. Us case mein **Hash Map** use kiya jaata hai.

---
