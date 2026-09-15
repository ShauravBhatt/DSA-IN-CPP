# LeetCode 852 — Peak Index in a Mountain Array

## Problem ko pehle feel karo

Bhai is problem ko dekhte hi code par jump nahi karna.

Pehle array ko **mountain** ki tarah imagine karo.

```text
[0, 3, 8, 9, 5, 2]

            9
           / \
          /   \
       8       5
      /         \
     3           2
    /
   0
```

Array pehle **increase** hota hai:

```text
0 < 3 < 8 < 9
```

Phir **decrease** hota hai:

```text
9 > 5 > 2
```

Beech ka highest element `9` **peak element** hai.

Question humein peak ki **value nahi**, uska **index** return karne ko bolta hai.

Important guarantee:

> Array already ek valid mountain array hai, so peak exist karegi hi.

---

# 1. Mountain Array actually hota kya hai?

Suppose:

```text
[1, 2, 4, 7, 5, 3]
```

Yahan:

```text
1 < 2 < 4 < 7
7 > 5 > 3
```

So shape:

```text
Increasing       Decreasing
     /\
    /  \
   /    \
```

Peak woh element hai jo:

```text
left wale se bada
AND
right wale se bada
```

Example:

```text
[1, 2, 4, 7, 5, 3]
         ↑
        peak
```

At index `3`:

```text
arr[3] > arr[2]
arr[3] > arr[4]
```

Answer:

```text
3
```

---

# 2. Sabse pehla solution — Linear Search

Natural thought:

> "Bhai ek-ek element check karte hain. Jahan current element apne left aur right dono se bada mil gaya, wahi peak."

For example:

```text
[0, 3, 8, 9, 5, 2]
```

Check:

```text
3 → peak? No
8 → peak? No
9 → peak? Yes
```

Time:

```text
O(n)
```

Ye solution logically correct hai.

Lekin problem mein humein **O(log n)** solution chahiye.

Yahin se Binary Search ka thought aana chahiye.

---

# 3. Binary Search yahan kyun sochni hai?

Normally hum Binary Search ko sorted array ke saath associate karte hain.

Lekin yahan ek interesting cheez hai:

```text
[0, 3, 8, 9, 5, 2]
```

Pura array sorted nahi hai.

Actually:

```text
0 < 3 < 8 < 9
```

first part increasing hai.

Then:

```text
9 > 5 > 2
```

second part decreasing hai.

So array ke andar **ordered structure** hai.

Question ye nahi hona chahiye:

> "Pura array sorted hai kya?"

Better question:

> **"Kya main har step par decide kar sakta hoon ki peak left mein hogi ya right mein?"**

Agar haan, Binary Search possible hai.

Aur yahan exactly wahi ho sakta hai.

---

# 4. Main Observation — `mid` ko uske next element se compare karo

Suppose:

```text
[0, 3, 8, 9, 5, 2]
```

Hum `mid` par aaye:

```text
[0, 3, 8, 9, 5, 2]
         ↑
        mid
```

Suppose:

```text
arr[mid] = 8
arr[mid + 1] = 9
```

Compare:

```text
8 < 9
```

Ab socho.

Hum mountain ke kis side par hain?

```text
       9
      /
     /
    8
```

Hum **increasing slope** par hain.

Matlab hum abhi peak tak pahunche hi nahi.

Peak kahan hogi?

```text
RIGHT
```

Because array abhi increase kar raha hai.

So:

```cpp
low = mid + 1;
```

---

# 5. Ye decision itna powerful kyun hai?

Isko properly feel karo.

Suppose:

```text
arr[mid] < arr[mid + 1]
```

Example:

```text
    /
   /
  ↑
 mid
```

Matlab `mid` ke baad wala element aur bada hai.

Toh `mid` definitely peak nahi hai.

Aur usse bhi important:

> **Peak `mid` ke left mein nahi ho sakti.**

Kyun?

Mountain mein peak ke baad values decrease hoti hain.

Agar `mid < mid+1` hai, toh hum abhi bhi climb kar rahe hain.

Climb chal rahi hai → peak aage hai.

Therefore:

```text
left side ❌
mid       ❌
right     ✓
```

So:

```cpp
low = mid + 1;
```

---

# 6. Ab opposite case dekho

Suppose:

```text
arr[mid] > arr[mid + 1]
```

Matlab:

```text
       9
      / \
     /   \
    8     5
          ↑
```

Hum **decreasing slope** par aa chuke hain.

Matlab peak already cross ho chuki hai, ya `mid` khud peak ho sakta hai.

So peak:

```text
LEFT side
OR
mid itself
```

mein ho sakti hai.

Right side ko safely discard kar sakte hain.

Therefore:

```cpp
high = mid;
```

Notice:

```cpp
high = mid;
```

not:

```cpp
high = mid - 1;
```

Kyun?

Because `mid` itself peak ho sakta hai.

---

# 7. Dono cases ko ek saath feel karo

### Case 1 — Increasing slope

```cpp
arr[mid] < arr[mid + 1]
```

Visual:

```text
      /
     /
    /
   ↑
  mid
```

Hum **upar ja rahe hain**.

Peak aage hai.

```text
Search → RIGHT
```

Therefore:

```cpp
low = mid + 1;
```

---

### Case 2 — Decreasing slope

```cpp
arr[mid] > arr[mid + 1]
```

Visual:

```text
    \
     \
      \
       ↓
      mid
```

Hum **neeche aa rahe hain**.

Peak left mein ya `mid` par hai.

```text
Search → LEFT / MID
```

Therefore:

```cpp
high = mid;
```

---

# 8. Normal Binary Search se difference

Normal Binary Search:

```text
arr[mid] == target?
        ↓
target < arr[mid]?
        ↓
left / right
```

Yahan target hi nahi hai.

Humein **peak** find karni hai.

So question change kar dete hain:

```text
arr[mid] < arr[mid + 1] ?
        ↓
    increasing
        ↓
   peak is RIGHT
```

Otherwise:

```text
arr[mid] > arr[mid + 1]
        ↓
    decreasing
        ↓
   peak is LEFT or MID
```

Ye **modified Binary Search** hai.

---

# 9. Complete Dry Run

Let's take:

```text
arr = [0, 3, 8, 9, 5, 2]
```

Indexes:

```text
index:  0  1  2  3  4  5
value:  0  3  8  9  5  2
```

Initial:

```text
low = 0
high = 5
```

Mid:

```text
mid = 0 + (5 - 0) / 2
mid = 2
```

So:

```text
arr[mid]     = 8
arr[mid + 1] = 9
```

Compare:

```text
8 < 9
```

Increasing slope.

So peak right mein hogi.

```text
low = mid + 1
low = 3
```

Search space:

```text
[9, 5, 2]
 ↑     ↑
low   high
```

---

## Step 2

```text
low = 3
high = 5

mid = 4
```

Now:

```text
arr[mid]     = 5
arr[mid + 1] = 2
```

Compare:

```text
5 > 2
```

Ab decreasing slope hai.

Matlab peak left mein ya `mid` par hai.

So:

```text
high = mid
high = 4
```

Search space:

```text
[9, 5]
 ↑  ↑
low high
```

---

## Step 3

```text
low = 3
high = 4

mid = 3
```

Now:

```text
arr[mid]     = 9
arr[mid + 1] = 5
```

Again:

```text
9 > 5
```

So:

```text
high = mid
high = 3
```

Now:

```text
low = 3
high = 3
```

Sirf ek candidate bacha:

```text
index = 3
```

And:

```text
arr[3] = 9
```

is the peak.

Answer:

```text
3
```

---

# 10. Yahan ek beautiful Binary Search idea hai

Normal Binary Search mein eventually:

```text
low == high
```

means one candidate remains.

Yahan bhi exactly same philosophy hai.

Hum har iteration mein:

```text
wrong half discard
```

karte ja rahe hain.

Eventually:

```text
low == high
```

and because mountain array mein peak guaranteed hai:

> **Jo single index bacha hai, wahi peak hai.**

So:

```cpp
return low;
```

---

# 11. `high = mid` kyun, `mid - 1` kyun nahi?

Ye bahut important hai.

Suppose:

```text
[1, 4, 7, 9, 6, 2]
```

Agar:

```text
mid = 3
arr[mid] = 9
arr[mid+1] = 6
```

Then:

```text
9 > 6
```

We know we're on the decreasing side.

But kya `mid = 3` peak ho sakta hai?

**YES.**

Actually:

```text
9 > 7
9 > 6
```

So `9` itself is peak.

Agar hum likh dete:

```cpp
high = mid - 1;
```

toh hum peak ko hi throw kar dete.

Isliye:

```cpp
high = mid;
```

`mid` ko candidate banaye rakhta hai.

---

# 12. `low = mid + 1` kyun?

Opposite case:

```text
arr[mid] < arr[mid + 1]
```

Suppose:

```text
mid = 2

arr[2] = 8
arr[3] = 9
```

`mid` peak nahi ho sakta because:

```text
arr[mid + 1] > arr[mid]
```

Aur peak `mid` ke left mein bhi nahi ho sakti because hum abhi increasing slope par hain.

So:

```text
mid + left side → impossible
```

Therefore:

```cpp
low = mid + 1;
```

Yahan `mid` ko include karne ki koi need nahi.

---

# 13. Edge Case — `mid + 1` safe kaise hai?

Hum compare karte hain:

```cpp
arr[mid] < arr[mid + 1]
```

Toh:

```text
mid + 1
```

valid index hona chahiye.

Isliye search space ko initially:

```cpp
low = 1;
high = arr.size() - 2;
```

rakhna clean hai.

Then:

```text
mid <= n - 2
```

guarantee hota hai, so:

```text
mid + 1 <= n - 1
```

and `arr[mid + 1]` safe hai.

---

# 14. First aur Last Index ko ignore kyun kar sakte hain?

Mountain array mein:

```text
first element = peak ❌
last element  = peak ❌
```

Peak beech mein hoti hai.

Isliye:

```cpp
int low = 1;
int high = arr.size() - 2;
```

use kar sakte hain.

Isse `mid - 1`, `mid`, aur `mid + 1` safely available rehte hain.

---

# 15. Ek aur Dry Run

Array:

```text
[1, 2, 4, 6, 9, 7, 3]
```

Visual:

```text
             9
            / \
           /   \
          /     \
       6         7
      /           \
     4             3
    /
   2
  /
 1
```

Suppose `mid` yahan hai:

```text
[1, 2, 4, 6, 9, 7, 3]
          ↑
         mid
```

Compare:

```text
6 < 9
```

Hum climb kar rahe hain.

Therefore:

```text
peak → RIGHT
```

So:

```cpp
low = mid + 1;
```

Ab maan lo next search space:

```text
[9, 7, 3]
```

Mid:

```text
7
```

Compare:

```text
7 > 3
```

Ab descent start ho chuka.

Therefore:

```text
peak → LEFT or MID
```

So:

```cpp
high = mid;
```

Eventually `9` wala index bachega.

---

# 16. Actual Binary Search intuition

Is problem ko solve karte waqt tumhare dimaag mein ye line honi chahiye:

> **"Main peak ko directly search nahi kar raha. Main ye identify kar raha hoon ki main mountain ke kis slope par khada hoon."**

Then:

```text
Increasing slope
arr[mid] < arr[mid+1]
        ↓
Peak abhi aage hai
        ↓
RIGHT
```

and:

```text
Decreasing slope
arr[mid] > arr[mid+1]
        ↓
Peak already left/mid mein hai
        ↓
LEFT / MID
```

Bas isi observation se `O(log n)` aa jaata hai.

---

# 17. Pseudocode

```text
low = 1
high = n - 2

while low < high:

    mid = low + (high - low) / 2

    if arr[mid] < arr[mid + 1]:

        # Increasing slope
        # Peak is on the right
        low = mid + 1

    else:

        # Decreasing slope
        # Peak is on the left or at mid
        high = mid

return low
```

---

# 18. Flowchart

```text
              Start
                ↓
        low = 1, high = n-2
                ↓
          low < high ?
           /       \
         YES        NO
          ↓          ↓
        Find mid   return low
          ↓
   arr[mid] < arr[mid+1] ?
       /             \
     YES              NO
      ↓                ↓
Increasing          Decreasing
slope               slope
      ↓                ↓
Peak is RIGHT      Peak is LEFT
      ↓             or MID
low = mid + 1          ↓
                     high = mid
          \           /
             Repeat
```

This flowchart shows that we only need to determine whether `mid` lies on the increasing or decreasing side of the mountain.

---

# 19. Final Code

```cpp
class Solution {
public:
    int peakIndexInMountainArray(vector<int>& arr) {

        int low = 1;
        int high = arr.size() - 2;

        while (low < high) {

            int mid = low + (high - low) / 2;

            // Increasing slope
            if (arr[mid] < arr[mid + 1]) {
                low = mid + 1;
            }

            // Decreasing slope
            else {
                high = mid;
            }
        }

        return low;
    }
};
```

---

# 20. Code ko story ki tarah read karo

```cpp
int low = 1;
int high = arr.size() - 2;
```

**"Peak first/last index par nahi ho sakti, so middle region search karo."**

```cpp
while (low < high)
```

**"Jab tak multiple possible peak indices hain, search continue karo."**

```cpp
int mid = low + (high - low) / 2;
```

**"Mountain ko beech se inspect karo."**

```cpp
if (arr[mid] < arr[mid + 1])
```

**"Agar next value badi hai, toh hum abhi climb kar rahe hain."**

```cpp
low = mid + 1;
```

**"Peak aage hai."**

```cpp
else
```

**"Agar next value chhoti hai, toh descent start ho chuka hai."**

```cpp
high = mid;
```

**"Peak left mein ya mid par ho sakti hai, so mid ko candidate rakho."**

Finally:

```cpp
return low;
```

**"Ab sirf ek possible position bachi hai — wahi peak hai."**

---

# 21. Complexity

Har iteration mein search space roughly half ho raha hai:

```text
n
↓
n/2
↓
n/4
↓
n/8
↓
...
↓
1
```

Therefore:

```text
Time Complexity  = O(log n)
Space Complexity = O(1)
```

---

# 22. Common Loopholes / Mistakes

## Mistake 1 — `high = mid - 1`

Wrong:

```cpp
high = mid - 1;
```

Why?

Because decreasing slope mein `mid` itself peak ho sakta hai.

Correct:

```cpp
high = mid;
```

---

## Mistake 2 — Increasing slope mein `low = mid`

Wrong:

```cpp
low = mid;
```

Agar:

```text
arr[mid] < arr[mid+1]
```

toh `mid` definitely peak nahi hai.

Correct:

```cpp
low = mid + 1;
```

---

## Mistake 3 — `mid + 1` boundary ignore karna

Agar `mid = n-1` ho gaya toh:

```cpp
arr[mid + 1]
```

invalid hoga.

Isliye search space ko:

```cpp
high = n - 2;
```

se restrict karna useful hai.

---

## Mistake 4 — Linear Search par ruk jaana

Linear search correct hai:

```text
O(n)
```

But question ka important constraint:

```text
O(log n)
```

hai.

So mountain structure ko exploit karna zaroori hai.

---

## Mistake 5 — Sirf peak condition check karte rehna

Tum har `mid` par:

```cpp
arr[mid] > arr[mid-1]
&&
arr[mid] > arr[mid+1]
```

check karke peak find kar sakte ho.

But uske baad actual important question hai:

> **"Agar mid peak nahi hai, toh next search space kahan hona chahiye?"**

Isi question ka answer Binary Search deta hai.

---

# 23. Is problem ka real Binary Search pattern

Ye problem ek important lesson sikhati hai:

> **Binary Search ke liye hamesha "sorted array + target" zaroori nahi hota.**

Sometimes tumhare paas koi **directional / monotonic property** hoti hai.

Yahan property hai:

```text
Increasing → Peak → Decreasing
```

Aur `mid` aur `mid+1` compare karke hum determine kar sakte hain:

```text
I'm still climbing
OR
I've started descending
```

Once we know that, peak ki direction known hai.

That is enough for Binary Search.

---

# 24. Practice — bina code dekhe

### Question 1

```text
arr = [0, 2, 5, 9, 7, 4, 1]
```

Find:

```text
low = ?
high = ?
mid = ?
arr[mid] = ?
arr[mid+1] = ?

Increasing ya decreasing slope?

Peak left mein hai ya right mein?
```

---

### Question 2

```text
arr = [1, 3, 7, 12, 10, 6, 2]
```

At each iteration only answer:

```text
arr[mid] < arr[mid+1] ?
```

Then decide:

```text
RIGHT
or
LEFT / MID
```

---

### Question 3

```text
arr = [2, 5, 8, 11, 9, 4]
```

Without looking at the code, explain:

> Agar `arr[mid] > arr[mid+1]` ho gaya, toh `high = mid` kyun karna hai?

Agar iska answer tum apni language mein explain kar pa rahe ho, toh problem genuinely samajh aa gayi hai.

---

# Final Thought

LeetCode 852 ko formula ki tarah yaad mat karo:

```cpp
if (arr[mid] < arr[mid + 1])
    low = mid + 1;
else
    high = mid;
```

Isko mountain ki movement ki tarah yaad rakho:

```text
        Peak
       /    \
      /      \
  climbing   falling
      ↑        ↓
    RIGHT    LEFT/MID
```

**"Agar main abhi upar ja raha hoon, peak aage hai. Agar main neeche aa raha hoon, peak peeche ya mere upar hi hai."**

Bas bhai — isi thought ko code mein convert kiya hai.
