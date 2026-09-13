# Binary Search — Part 1
## From Linear Search to the Binary Search Idea

Binary Search ko samajhne se pehle ek simple question:

> Agar mere paas ek **sorted array** hai, aur mujhe ek particular number find karna hai, toh kya mujhe har element ko one-by-one check karna zaroori hai?

Example:

```text
[10, 20, 30, 40, 50, 60, 70, 80]
```

Target:

```text
70
```

Simple approach:

```text
10 → no
20 → no
30 → no
40 → no
50 → no
60 → no
70 → YES
```

Ye **Linear Search** hai.

Problem ye hai ki array bada hone par hume bahut saare elements check karne pad sakte hain.

---

# 1. Linear Search Ki Problem

Suppose:

```text
n = 1,000,000
```

Worst case mein Linear Search ko almost:

```text
1,000,000 elements
```

check karne pad sakte hain.

So:

```text
Time Complexity = O(n)
```

Lekin yahan ek important cheez already available hai:

> Array **sorted** hai.

Sorted order hume extra information deta hai.

Isi information ka use karke hum search ko bahut fast bana sakte hain.

---

# 2. Sorted Array Hume Kya Extra Information De Raha Hai?

Consider:

```text
[10, 20, 30, 40, 50, 60, 70, 80, 90]
```

Target:

```text
70
```

Agar hum middle element check karein:

```text
[10, 20, 30, 40, 50, 60, 70, 80, 90]
                  ↑
                 50
```

Now:

```text
70 > 50
```

Because array sorted hai, hum confidently bol sakte hain:

> `70` left side mein nahi ho sakta.

So:

```text
10, 20, 30, 40, 50
```

ko dobara check karne ki need nahi.

Ek comparison se humne almost half search space eliminate kar diya.

**Yahi Binary Search ka main idea hai.**

---

# 3. Binary Search Actually Karta Kya Hai?

Binary Search repeatedly:

> **Current search space ko half karta hai.**

Example:

```text
[10, 20, 30, 40, 50, 60, 70, 80, 90]
                  ↑
                 50
```

Target:

```text
70
```

Since:

```text
70 > 50
```

left half impossible:

```text
[10, 20, 30, 40, 50] ❌
```

Ab sirf:

```text
[60, 70, 80, 90]
```

search karna hai.

Again middle check karo.

```text
70
```

Mil gaya.

So Binary Search ka core:

```text
Check middle
    ↓
Decide which half is possible
    ↓
Discard the other half
    ↓
Repeat
```

---

# 4. `low`, `high`, `mid`

Binary Search mein generally hum teen variables track karte hain:

```text
low
high
mid
```

Simple meaning:

```text
low  → current search area ka starting index
high → current search area ka ending index
mid  → current search area ka middle index
```

Example:

```text
[10, 20, 30, 40, 50, 60, 70]
```

Indexes:

```text
 0   1   2   3   4   5   6
```

Initially:

```text
low = 0
high = 6
```

Middle:

```text
mid = 3
```

So:

```text
Index:   0   1   2   3   4   5   6
        ┌───┬───┬───┬───┬───┬───┬───┐
        │10 │20 │30 │40 │50 │60 │70 │
        └───┴───┴───┴───┴───┴───┴───┘
         ↑           ↑               ↑
        low         mid             high
```

---

# 5. Target `mid` Se Bada Ho

Suppose:

```text
target = 70
```

and:

```text
arr[mid] = 40
```

Compare:

```text
70 > 40
```

Since array sorted hai, target right side mein ho sakta hai.

Left side impossible hai.

So:

```cpp
low = mid + 1;
```

Why `mid + 1`?

Because `mid` bhi already check kar chuke hain.

Agar:

```text
arr[mid] = 40
```

aur target `70` hai, toh `mid` dobara check karne ki need nahi.

So next possible position:

```text
mid + 1
```

---

# 6. Target `mid` Se Chhota Ho

Suppose:

```text
target = 20
```

and:

```text
arr[mid] = 40
```

Now:

```text
20 < 40
```

Sorted array hone ki wajah se target right side mein nahi ho sakta.

So right side discard.

We do:

```cpp
high = mid - 1;
```

Again `mid` already check ho chuka hai, so:

```text
mid - 1
```

tak hi possible search space rahega.

---

# 7. Target `mid` Ke Equal Ho

Agar:

```text
target == arr[mid]
```

then:

```text
Target found.
```

Search stop.

```text
return mid;
```

So every iteration mein basically three cases:

```text
target < arr[mid]
        ↓
   left side

target == arr[mid]
        ↓
      found

target > arr[mid]
        ↓
  right side
```

---

# 8. Why Must the Array Be Sorted?

Ye bahut important hai.

Suppose:

```text
[10, 70, 20, 40, 90, 30, 60]
```

Middle:

```text
40
```

Target:

```text
70
```

We know:

```text
70 > 40
```

But kya hum bol sakte hain ki `70` definitely right side mein hai?

**No.**

`70` left side mein bhi ho sakta hai.

Because array sorted nahi hai.

So Binary Search ka elimination logic break ho gaya.

Sorted array hume ye confidence deta hai:

```text
target < middle
→ right side impossible

target > middle
→ left side impossible
```

Without sorted order, hum safely half eliminate nahi kar sakte.

---

# 9. Search Space

Binary Search ko ek simple idea se dekho:

> Hum poore array ko baar-baar search nahi kar rahe. Hum sirf current **possible search area** mein search kar rahe hain.

Initially:

```text
[10, 20, 30, 40, 50, 60, 70, 80]
 ↑                                      ↑
low                                   high
```

Suppose middle `40` hai and target `70`.

Left side impossible:

```text
[10, 20, 30, 40] ❌
```

New search space:

```text
[50, 60, 70, 80]
 ↑              ↑
low            high
```

Then again half eliminate karenge.

So:

```text
Large search space
        ↓
Smaller search space
        ↓
Even smaller search space
        ↓
Target found / search space empty
```

---

# 10. Complete Dry Run

Array:

```text
[10, 20, 30, 40, 50, 60, 70, 80, 90]
```

Target:

```text
70
```

### Step 1

Initially:

```text
low = 0
high = 8
```

Middle:

```text
mid = 4
arr[mid] = 50
```

Compare:

```text
70 > 50
```

So left side discard.

```text
low = mid + 1
low = 5
```

Now:

```text
low = 5
high = 8
```

Search space:

```text
60  70  80  90
↑           ↑
low        high
```

### Step 2

Middle:

```text
mid = 6
arr[mid] = 70
```

Compare:

```text
70 == 70
```

Found.

Answer:

```text
index = 6
```

Only two middle checks were needed.

---

# 11. What If Target Doesn't Exist?

Same array:

```text
[10, 20, 30, 40, 50, 60, 70, 80, 90]
```

Target:

```text
75
```

Initially:

```text
low = 0
high = 8
```

Middle:

```text
50
```

Since:

```text
75 > 50
```

move right:

```text
low = 5
```

Now search:

```text
[60, 70, 80, 90]
```

Middle:

```text
70
```

Since:

```text
75 > 70
```

move right:

```text
low = 7
```

Now:

```text
[80, 90]
```

Middle:

```text
80
```

Since:

```text
75 < 80
```

move left:

```text
high = 6
```

Now:

```text
low = 7
high = 6
```

So:

```text
low > high
```

Search space empty ho gaya.

Therefore:

```text
Target does not exist.
```

Ye condition later code mein important hogi.

---

# 12. Why Is It Called Binary Search?

Binary ka basic idea hai:

> Search space ko two parts mein divide karna and only one possible part continue karna.

```text
             Search Space
                  ↓
                middle
               /                    /                impossible     possible
            ❌             ✓
```

Hum actually do arrays create nahi karte.

Sirf:

```text
low
high
```

change karte hain.

---

# 13. Binary Search Ki Speed

Suppose:

```text
n = 16
```

Every step roughly half:

```text
16
↓
8
↓
4
↓
2
↓
1
```

So around 4–5 decisions.

For:

```text
n = 1,000,000
```

roughly:

```text
1,000,000
↓
500,000
↓
250,000
↓
125,000
↓
...
↓
1
```

Approximately:

```text
log₂(1,000,000) ≈ 20
```

So comparison:

```text
Linear Search
→ potentially 1,000,000 checks

Binary Search
→ roughly 20 checks
```

Isi wajah se sorted data par Binary Search extremely powerful hai.

---

# 14. Basic Binary Search Ki Core Conditions

Basic Binary Search ke liye do important cheezein:

### 1. Data ordered/sorted hona chahiye

Taaki hum comparison ke basis par ek side eliminate kar sakein.

### 2. Hum confidently half eliminate kar sakein

Actual important pattern ye hai:

> **Can I make a reliable decision that one half of my current search space is impossible?**

Sorted array mein answer yes hota hai.

Later difficult Binary Search problems mein array directly sorted na bhi ho, but hum kisi aur property ke basis par search space eliminate kar sakte hain.

---

# Practice

Abhi code mat likho.

Given:

```text
arr = [3, 7, 11, 18, 24, 31, 42, 55, 68]
```

Target:

```text
42
```

Manually find:

```text
Step 1:
low = ?
high = ?
mid = ?
arr[mid] = ?

Step 2:
low = ?
high = ?
mid = ?
arr[mid] = ?

Step 3:
target found at index = ?
```

Har step mein pehle ye decide karo:

> **Kaunsa half impossible hai, and why?**
