# Maximum Subarray Sum — Building the Logic (Brute Force → Better → Kadane)

## Problem
Leetcode Link: https://leetcode.com/problems/maximum-subarray/

Given an array, find the **maximum sum of any contiguous (continuous) subarray**.

Example:

```cpp
arr = {10, -5, 4, 3, -2, 7, -6, -5}
```

Before jumping to the solution, let's ask a simple question.

> **Agar mujhe answer hi nahi pata, to main shuru kaha se karunga?**

Sabse obvious approach se.

---

# Approach 1 : Generate Every Possible Subarray (Brute Force)

Sabse pehle hume saari possible subarrays dekhni hongi.

Lekin ek doubt aata hai.

> **Subarray banegi kaise?**

Ek subarray banane ke liye sirf do cheezein decide karni hoti hain.

* Starting Index
* Ending Index

Bas.

Maan lo array hai

```text
Index : 0   1   2   3
Value : 5   2   8   1
```

Agar start `0` hai, to end kya-kya ho sakta hai?

```text
0

0 → 1

0 → 2

0 → 3
```

Yaani subarrays banengi

```text
5

5 2

5 2 8

5 2 8 1
```

Ab start ko `1` kar do.

```text
2

2 8

2 8 1
```

Ab start ko `2` kar do.

```text
8

8 1
```

Isi idea ko code mein likha gaya hai.

```cpp
for (int start = 0; start < arr.size(); start++)
```

Ye loop sirf ek kaam karta hai.

> **"Subarray ki starting position choose karo."**

---

Ab ek aur question.

> **Start to mil gaya. End kaun decide karega?**

Uske liye second loop.

```cpp
for (int end = start; end < arr.size(); end++)
```

Dhyan do.

`end` hamesha `start` se hi shuru ho raha hai.

Kyuki ending kabhi starting se pehle nahi ho sakti.

Ye loop ek hi subarray ko dheere-dheere bada karta hai.

```text
4

4 3

4 3 -2

4 3 -2 7
```

Har iteration mein sirf ek element add ho raha hai.

---

Ab teesra question.

> **Start aur End dono mil gaye. Ab beech ke elements kaise dekhenge?**

Uske liye third loop.

```cpp
for (int i = start; i <= end; i++)
{
    cout << arr[i];
}
```

Ye `start` se `end` tak travel karta hai.

Agar

```text
start = 2

end = 5
```

to ye visit karega

```text
Index 2

↓

Index 3

↓

Index 4

↓

Index 5
```

Isi tarah ek complete subarray print hoti hai.

Ab teeno loops ka purpose clear hai.

| Loop   | Responsibility                |
| ------ | ----------------------------- |
| First  | Starting index choose karna   |
| Second | Ending index choose karna     |
| Third  | Beech ke elements visit karna |

---

## Problem

Ab ek aur question.

> **Kya har baar poori subarray dobara traverse karna zaroori hai?**

Socho.

Subarray hai

```text
10 -5 4
```

Iska sum hai

```text
9
```

Ab agli subarray hai

```text
10 -5 4 3
```

Kya firse

```text
10 + (-5) + 4 + 3
```

calculate karoge?

Nahi.

Pehla sum already pata hai.

Sirf naya element add karna hai.

Yahi observation hume next approach tak le jaati hai.

---

# Approach 2 : Remove Repeated Work

Code dekho.

```cpp
int maxSum = INT_MIN;

for (int start = 0; start < arr.size(); start++)
{
    int currentSum = 0;

    for (int end = start; end < arr.size(); end++)
    {
        currentSum += arr[end];
        maxSum = max(currentSum, maxSum);
    }
}
```

Sabse pehle ye line.

```cpp
int currentSum = 0;
```

Question.

> **Ye first loop ke andar hi kyu hai?**

Kyuki har naya `start` ek nayi journey hai.

Agar pehle

```text
10

10 -5

10 -5 4
```

ka sum nikal rahe the,

aur ab `start = 1` ho gaya,

to purana sum kisi kaam ka nahi.

Isliye `currentSum` ko reset karte hain.

---

Ab ye line.

```cpp
currentSum += arr[end];
```

Ye poori approach ka heart hai.

Maan lo

```text
10
```

Current Sum = 10

Agli subarray

```text
10 -5
```

Bas

```text
10 + (-5)
```

kar diya.

Current Sum = 5

Agli subarray

```text
10 -5 4
```

Bas

```text
5 + 4
```

Current Sum = 9

Har baar sirf **ek naya element** add ho raha hai.

Isi wajah se third loop ki zarurat hi nahi padti.

Time Complexity

```text
O(n³)

↓

O(n²)
```

---

Ab ek aur question.

> **Kya first loop bhi hata sakte hain?**

Yahin se Kadane's Algorithm shuru hoti hai.

---

# Approach 3 : Kadane's Algorithm

Code

```cpp
int currSum = 0;
int maxSum = INT_MIN;

for (int i = 0; i < arr.size(); i++)
{
    currSum += arr[i];

    maxSum = max(currSum, maxSum);

    if (currSum < 0)
    {
        currSum = 0;
    }
}
```

Is algorithm ko samajhne ke liye ek situation socho.

Current running sum hai

```text
-8
```

Next element hai

```text
5
```

Ab do choices hain.

### Choice 1

Purani subarray continue karo.

```text
-8 + 5 = -3
```

### Choice 2

Yahin se nayi subarray shuru karo.

```text
5
```

Kaunsi better hai?

Clearly,

```text
5
```

Ab ek important observation.

> **Agar running sum already negative hai, to wo future ko help karega ya hurt?**

Hamesha hurt karega.

Negative sum future ke har answer ko chhota karega.

To usse carry hi kyu kare?

Usse wahi chhod do.

Isi thought ko code mein likha gaya hai.

```cpp
if (currSum < 0)
{
    currSum = 0;
}
```

Iska matlab ye nahi hai ki negative numbers allowed nahi hain.

Iska matlab sirf itna hai ki

> **Negative running sum ko future mein carry nahi karna.**

---

## Dry Run

```text
Array

10  -5  4  3  -2  7  -6  -5
```

| Element | currSum | maxSum |
| ------: | ------: | -----: |
|      10 |      10 |     10 |
|      -5 |       5 |     10 |
|       4 |       9 |     10 |
|       3 |      12 |     12 |
|      -2 |      10 |     12 |
|       7 |      17 |     17 |
|      -6 |      11 |     17 |
|      -5 |       6 |     17 |

Notice one thing.

`currSum` kabhi negative hi nahi hua.

Isliye reset ki zarurat nahi padi.

---

Ab edge case dekhte hain.

```text
-4 2 3
```

| Element | currSum | maxSum |
| ------: | ------: | -----: |
|      -4 |      -4 |     -4 |
|   Reset |       0 |     -4 |
|       2 |       2 |      2 |
|       3 |       5 |      5 |

Agar reset na karte,

to

```text
-4 + 2 + 3 = 1
```

Lekin agar negative sum ko yahin chhod diya,

to

```text
2 + 3 = 5
```

Jo clearly better answer hai.

Isi observation ki wajah se Kadane's Algorithm sirf ek loop mein kaam kar leti hai.

---

## Why `maxSum` is updated before resetting?

Code ka order dekho.

```cpp
currSum += arr[i];

maxSum = max(currSum, maxSum);

if(currSum < 0)
{
    currSum = 0;
}
```

Suppose array sirf ek hi element ka hai.

```text
[-2]
```

Pehle compare karenge.

```text
maxSum = -2
```

Uske baad reset karenge.

Agar pehle reset kar dete,

to answer galat ho jaata.

Isliye line ka order bhi algorithm ka part hai.