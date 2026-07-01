# Majority Element (Brute Force → Sorting → Moore's Voting Algorithm)

## Problem
Leetcode Link: https://leetcode.com/problems/majority-element/


Given an integer array, return the element whose frequency is **greater than [n/2]**.

If no such element exists, return that there is no majority element.

Example:

```cpp
arr = {1, 1, 2, 1, 2}
```

Frequency

```text
1 → 3 times

2 → 2 times
```

Array size

```text
n = 5
```

Majority condition

```text
Frequency > n/2

3 > 2 ✅
```

Answer

```text
1
```

---

# Approach 1 : Brute Force

Whenever we don't know any optimization, the first thought should be

> **"Har element ki frequency nikal kar dekh lete hain."**

Exactly yahi idea brute force mein use hota hai.

Code

```cpp
for (int i = 0; i < length; i++)
{
    int count = 0;

    for (int j = 0; j < length; j++)
    {
        if (arr[i] == arr[j])
        {
            count++;
        }
    }

    if (count > length / 2)
    {
        majorityElement = arr[i];
        break;
    }
}
```

---

## Logic

Outer loop ek element choose karta hai.

```text
First

1

↓

Again

1

↓

2

↓

1

↓

2
```

Ab question aata hai.

> **Is element ki frequency kitni hai?**

Uske liye inner loop poori array traverse karta hai.

Example

```text
Current Element = 1
```

Compare with every element.

```text
1 == 1 ✅

1 == 1 ✅

1 == 2 ❌

1 == 1 ✅

1 == 2 ❌
```

Total Frequency

```text
3
```

Ab check karte hain

```text
3 > 5/2

3 > 2 ✅
```

Answer mil gaya.

---

## Problem

Notice something.

Agar array mein

```text
1000
```

elements hain,

to har element ke liye hum firse poori array traverse kar rahe hain.

Bahut repeated work ho raha hai.

Time Complexity

```text
O(n²)
```

Question.

> **Can we avoid counting the same element again and again?**

Yes.

---

# Approach 2 : Sorting

Observation.

Array hai

```text
1 1 2 1 2
```

Abhi same elements alag-alag jagah pade hain.

Frequency count karna difficult hai.

Question.

> **Agar same elements ek saath aa jaye to?**

Bas isi idea se sorting aati hai.

Sort karte hi array ban jaati hai.

```text
1 1 1 2 2
```

Ab frequency count karna bahut easy ho gaya.

Same values already together hain.

Isi observation ko code mein likha gaya hai.

```cpp
sort(arr.begin(), arr.end());
```

---

## Code Understanding

```cpp
int count = 1;
int ans = arr[0];
```

`ans`

Current number jiska count chal raha hai.

Initially

```text
1
```

`count`

Us number ki frequency.

Initially

```text
1
```

Kyuki first element already mil chuka hai.

---

Loop starts from index 1.

```cpp
for(int i=1;i<length;i++)
```

Question.

> **Current element previous element ke equal hai?**

```cpp
if(arr[i] == arr[i-1])
```

Agar equal hai,

iska matlab same number continue ho raha hai.

Frequency badha do.

```cpp
count++;
```

Example

```text
1 1 1 2 2
```

```text
1 == 1

count = 2
```

Again

```text
1 == 1

count = 3
```

---

Suppose next element

```text
2
```

Ab

```text
2 != 1
```

Matlab ek naya number start ho gaya.

Purani frequency ka koi use nahi.

Reset.

```cpp
ans = arr[i];
count = 1;
```

Ab counting dobara start.

---

Har iteration mein check karte hain.

```cpp
if(count > length/2)
```

Agar majority mil gayi,

answer return.

---

## Complexity

Sorting

```text
O(n log n)
```

Traversal

```text
O(n)
```

Overall

```text
O(n log n)
```

Question.

> **Can we solve it without sorting?**

Yes.

Aur wahi hai Moore's Voting Algorithm.

---

# Approach 3 : Moore's Voting Algorithm

Ye algorithm pehli baar dekhne par magic lagti hai.

Lekin actually ye sirf ek simple observation par based hai.

Us observation ko samajhte hain.

---

## Sabse Pehle Ek Question

Suppose array hai

```text
1 2
```

Ek baar

```text
1
```

Aaya.

Ek baar

```text
2
```

Aaya.

Dono ki frequency same hai.

Question.

> **Kya in dono mein se koi majority ban sakta hai?**

Nahi.

Dono ek dusre ko cancel kar dete hain.

Socho jaise election chal raha ho.

Ek vote mila

```text
1
```

ko.

Ek vote mila

```text
2
```

ko.

Result?

```text
Tie.
```

Kisi ka advantage nahi.

Dono eliminate.

---

Ab doosra example.

```text
1 2 1
```

Pair banao.

```text
1 2
```

Cancel.

Bach gaya.

```text
1
```

Ye bacha hua vote kis ka hai?

```text
1
```

Ab socho.

Majority element agar exist karta hai,

to uske votes itne zyada honge ki

sab opposite elements ke saath cancel hone ke baad bhi

wo bach hi jayega.

Yehi Moore's Voting ka core idea hai.

> **Different elements ek dusre ko cancel karte rehte hain. Majority element kabhi completely cancel nahi hota.**

---

## Ek Intuition

Suppose class mein

```text
7 Boys

3 Girls
```

Har baar

ek Boy aur ek Girl bahar chale jaate hain.

```text
Boy ❌

Girl ❌
```

Again

```text
Boy ❌

Girl ❌
```

Again

```text
Boy ❌

Girl ❌
```

Ab kya bacha?

```text
4 Boys
```

Majority group hamesha end mein bachta hai.

Exactly yahi Moore's Voting karta hai.

---

# Understanding the Variables

```cpp
int freq = 0;
int ans = 0;
```

`ans`

Current candidate.

Not final answer.

Sirf candidate.

`freq`

Candidate ke support mein current vote balance.

---

## Code Understanding

```cpp
for(int i=0;i<length;i++)
```

Array ko ek baar traverse karte hain.

---

### Step 1

```cpp
if(freq == 0)
{
    ans = arr[i];
}
```

Question.

> **Candidate kab change karte hain?**

Jab uske paas ek bhi vote na bache.

Agar

```text
freq = 0
```

Matlab purana candidate completely cancel ho chuka.

Ab next element ko candidate bana do.

---

### Step 2

```cpp
if(ans == arr[i])
{
    freq++;
}
```

Same candidate mila.

Support badh gaya.

Vote increase.

---

### Step 3

```cpp
else
{
    freq--;
}
```

Different element mila.

Ek vote cancel.

Support decrease.

Bas.

Algorithm mein aur kuch nahi ho raha.

---

# Dry Run

Array

```text
1 1 2 1 2
```

| Element | Candidate | Freq | Reason                      |
| ------- | --------- | ---- | --------------------------- |
| 1       | 1         | 1    | New Candidate               |
| 1       | 1         | 2    | Same Candidate              |
| 2       | 1         | 1    | Different → Cancel One Vote |
| 1       | 1         | 2    | Same Candidate              |
| 2       | 1         | 1    | Different → Cancel One Vote |

End mein

```text
Candidate = 1
```

Notice.

Frequency zero kabhi hui hi nahi.

Kyuki majority element continuously survive karta raha.

---

## Ek Difficult Example

```text
2 1 2 3 2 2 4
```

| Element | Candidate | Freq |
| ------- | --------- | ---- |
| 2       | 2         | 1    |
| 1       | 2         | 0    |
| 2       | 2         | 1    |
| 3       | 2         | 0    |
| 2       | 2         | 1    |
| 2       | 2         | 2    |
| 4       | 2         | 1    |

Notice kya hua.

Candidate baar-baar almost cancel hua.

Lekin end mein

```text
2
```

fir bhi bach gaya.

Yehi Moore's Voting ka proof hai.

Majority element ko poori tarah cancel karna possible hi nahi.

---

# Why Do We Count Again?

Question.

> **Agar candidate mil gaya, to direct answer return kyu nahi kar dete?**

Kyuki har problem guarantee nahi deti ki majority element exist karega.

Example

```text
1 2 3 4
```

Algorithm kisi ek candidate par end karega.

Lekin actually majority element hai hi nahi.

Isliye final verification zaroori hai.

Isi liye second traversal.

```cpp
int count = 0;

for(int ele : arr)
{
    if(ele == ans)
    {
        count++;
    }
}
```

Agar

```text
count > n/2
```

Tabhi answer valid hai.

Otherwise

```text
No Majority Element
```

---

# Final Optimal Code (Moore's Voting Algorithm)

```cpp
#include <iostream>
#include <vector>
using namespace std;

int main()
{
    vector<int> arr = {1, 1, 2, 1, 2};

    int n = arr.size();

    int candidate = 0;
    int freq = 0;

    // Phase 1 : Find Candidate
    for (int num : arr)
    {
        if (freq == 0)
        {
            candidate = num;
        }

        if (candidate == num)
        {
            freq++;
        }
        else
        {
            freq--;
        }
    }

    // Phase 2 : Verify Candidate
    int count = 0;

    for (int num : arr)
    {
        if (num == candidate)
        {
            count++;
        }
    }

    if (count > n / 2)
    {
        cout << "Majority Element : " << candidate;
    }
    else
    {
        cout << "No Majority Element";
    }

    return 0;
}
```

---

# Complexity

| Approach       | Time       | Space |
| -------------- | ---------- | ----- |
| Brute Force    | O(n²)      | O(1)  |
| Sorting        | O(n log n) | O(1)  |
| Moore's Voting | O(n)       | O(1)  |
