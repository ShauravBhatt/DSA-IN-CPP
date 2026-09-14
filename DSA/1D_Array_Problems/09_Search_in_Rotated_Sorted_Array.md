# Search in Rotated Sorted Array

## Problem ko pehle feel karo
Problem Link: https://leetcode.com/problems/search-in-rotated-sorted-array/description/

Humein ek **sorted ascending array** diya gaya tha, lekin array ko kisi point par rotate kar diya gaya.

Example:

```text
Original:
[1, 2, 3, 4, 5, 6, 7]

Rotate:
[4, 5, 6, 7, 1, 2, 3]
```

Target diya hai, aur humein uska index return karna hai.

Condition: **O(log n)** time.

---

# 1. Sabse pehla thought — Brute Force

Sabse natural approach:

> "Bhai ek-ek element check kar leta hoon."

```text
[4, 5, 6, 7, 1, 2, 3]
 ↑
check
```

Target mila → index return.

Worst case mein poora array traverse karna padega.

```text
Time = O(n)
```

Lekin problem specifically `O(log n)` maang rahi hai.

Toh yahan ek strong hint milta hai:

> **O(log n) dekhte hi Binary Search ke baare mein socho.**

---

# 2. Lekin normal Binary Search yahan fail kyun hoti hai?

Normal Binary Search mein hum ek assumption use karte hain:

```text
Array sorted hai
        ↓
mid ke comparison se
        ↓
ek poora half impossible declare kar sakte hain
```

Example:

```text
[1, 2, 3, 4, 5, 6, 7, 8, 9]
                ↑
               mid
```

Agar target `8` hai aur `mid = 5`:

```text
8 > 5
```

Sorted array hone ki wajah se hum confidently bol sakte hain:

```text
[1, 2, 3, 4, 5] ❌
```

Target left mein nahi ho sakta.

Simple.

---

## Ab rotated array dekho

```text
[6, 7, 8, 1, 2, 3, 4]
```

Ye globally sorted nahi hai.

Yahan:

```text
8 → 1
```

ke beech order break ho gaya.

Toh sirf:

```text
target > nums[mid]
```

dekhkar ye decide nahi kar sakte ki target normal sorted-array logic se kis side hoga.

**Hamari purani guarantee toot gayi.**

Lekin interesting part yahin se start hota hai.

---

# 3. Array rotated hai, phir bhi ek important property bachi hui hai

Example:

```text
[6, 7, 8, 1, 2, 3, 4]
```

Agar `mid` roughly `1` par hai:

```text
[6, 7, 8, 1 | 2, 3, 4]
             ↑
            mid
```

Left side:

```text
[6, 7, 8, 1]
```

Right side:

```text
[2, 3, 4]
```

Right side clearly sorted hai.

Aur left side mein rotation ka break hai.

Dusre example mein:

```text
[4, 5, 6, 7, 1, 2, 3]
```

mid ke around:

```text
[4, 5, 6, 7 | 1, 2, 3]
```

Left sorted hai.

So key observation:

> **Rotated sorted array mein har iteration par left half ya right half mein se kam se kam ek half sorted zaroor milega.**

Yehi poori problem ka main trick hai.

---

# 4. Ye property aati kahan se hai?

Isko ratna nahi hai. Imagine karo original sorted array:

```text
[1, 2, 3, 4, 5, 6, 7]
```

Rotation basically ek cut hai:

```text
[1, 2, 3 | 4, 5, 6, 7]
```

Phir pieces ko swap kar diya:

```text
[4, 5, 6, 7 | 1, 2, 3]
```

Bas **ek jagah order break hua**.

Isliye jab tum kisi `mid` par array ko do parts mein divide karte ho, dono parts ek saath broken nahi ho sakte.

Ek side ko break mil sakta hai.

Doosri side mein break nahi hoga.

Therefore:

```text
At least ONE half is sorted.
```

Ab humein isi sorted half ka fayda uthana hai.

---

# 5. Ab actual strategy build karte hain

Suppose:

```text
nums = [6, 7, 8, 1, 2, 3, 4]
target = 3
```

Hum:

```text
low = 0
high = 6
mid = 3
```

So:

```text
index:  0  1  2  3  4  5  6
        -----------------------
nums:   6  7  8  1  2  3  4
                 ↑
                mid
```

`nums[mid] = 1`.

Target `3` hai.

Ab pehle target == mid check karenge.

```text
1 == 3 ? No
```

Ab question:

> **Kaunsa half sorted hai?**

Left half:

```text
[6, 7, 8, 1]
```

Ye sorted nahi hai.

Toh right half sorted hona chahiye:

```text
[1, 2, 3, 4]
```

Exactly.

---

# 6. Sorted half mil gaya — ab uska kya karein?

Right half:

```text
[1, 2, 3, 4]
```

Iska range:

```text
1 → 4
```

Target:

```text
3
```

Kya `3` is range ke andar hai?

Yes.

```text
1 < 3 <= 4
```

Toh target right half mein ho sakta hai.

So:

```cpp
low = mid + 1;
```

Hum left side ko discard kar dete hain.

---

# 7. Agar target sorted half ke range mein NA ho?

Ye aur important case hai.

Suppose:

```text
nums = [6, 7, 8, 1, 2, 3, 4]
target = 7
```

Same:

```text
mid = 1
```

Right half sorted:

```text
[1, 2, 3, 4]
```

Target:

```text
7
```

Kya `7` `[1,4]` ke andar hai?

No.

Toh target right half mein ho hi nahi sakta.

Therefore:

```text
right half ❌
left half   ✓
```

So:

```cpp
high = mid - 1;
```

Yahi actual thinking hai.

---

# 8. Left half sorted kaise detect karte hain?

Condition:

```cpp
nums[low] <= nums[mid]
```

Kyun?

Normal sorted sequence mein:

```text
leftmost <= middle
```

Example:

```text
[4, 5, 6, 7]
 ↑     ↑
low   mid

4 <= 6 ✓
```

Agar ye true hai, left half sorted hai.

```cpp
if (nums[low] <= nums[mid])
```

---

# 9. Left half sorted hai — target usmein hai ya nahi?

Suppose:

```text
[4, 5, 6, 7, 0, 1, 2]
```

and:

```text
mid = 7
```

Left half:

```text
[4, 5, 6, 7]
```

sorted hai.

Ab target `5` hai.

Target left half ke range mein hai:

```text
4 <= 5 < 7
```

So target left mein ho sakta hai.

```cpp
high = mid - 1;
```

---

## Target left range mein nahi hai

Target `1` hai.

Left sorted range:

```text
4 → 7
```

`1` is range mein nahi hai.

Therefore:

```text
left half ❌
right half ✓
```

So:

```cpp
low = mid + 1;
```

---

# 10. Ek subtle point — `mid` ko range mein kyun exclude karte hain?

Hum start mein already check kar chuke hain:

```cpp
if (nums[mid] == target)
    return mid;
```

Matlab agar target `mid` par tha, hum already return kar chuke.

Isliye baad mein:

```text
left range:
nums[low] <= target < nums[mid]
```

and:

```text
right range:
nums[mid] < target <= nums[high]
```

use kar sakte hain.

---

# 11. Complete Decision Making

Har iteration mein bas ye questions poochne hain:

```text
1. mid nikalo
        ↓
2. nums[mid] == target?
        ↓
       YES → answer
        ↓ NO
3. Left half sorted hai?
        ↓
   nums[low] <= nums[mid]
        ↓
   ┌───────────────┐
   │               │
  YES              NO
   │               │
Left sorted    Right sorted
   │               │
Target range?  Target range?
   │               │
 YES / NO       YES / NO
   │     │       │     │
 left  right   right  left
```

Code baad mein isi decision tree ka translation hai.

---

# 12. Full Dry Run

Let's properly walk through:

```text
nums = [6, 7, 8, 1, 2, 3, 4]
target = 3
```

### Step 1

```text
low = 0
high = 6
mid = 3

nums[mid] = 1
```

Target `3` nahi hai.

Check left sorted:

```text
nums[low] <= nums[mid]

6 <= 1 ❌
```

So right half sorted:

```text
[1, 2, 3, 4]
```

Target `3` range mein hai:

```text
1 < 3 <= 4 ✓
```

Therefore:

```text
low = mid + 1
low = 4
```

New search space:

```text
[2, 3, 4]
 ↑     ↑
low   high
```

---

### Step 2

```text
low = 4
high = 6
mid = 5

nums[mid] = 3
```

Target:

```text
3 == 3
```

Mil gaya.

Return:

```text
index = 5
```

Notice:

Humne poore array ko scan nahi kiya.

Har step mein search space shrink hua.

That's why:

```text
O(log n)
```

---

# 13. Ek aur dry run — left half sorted

```text
nums = [4, 5, 6, 7, 0, 1, 2]
target = 5
```

Initial:

```text
low = 0
high = 6
mid = 3

nums[mid] = 7
```

Target `7` nahi hai.

Left sorted?

```text
nums[low] <= nums[mid]

4 <= 7 ✓
```

So:

```text
[4, 5, 6, 7]
```

sorted half hai.

Target `5` range mein hai?

```text
4 <= 5 < 7 ✓
```

So left jao:

```cpp
high = mid - 1;
```

Now:

```text
[4, 5, 6]
```

Next iteration mein target mil jayega.

---

# 14. Sabse important intuition

Normal Binary Search mein hum sochte the:

> **"Array sorted hai, isliye half eliminate kar sakta hoon."**

Rotated Binary Search mein thought thoda evolve hota hai:

> **"Poora array sorted nahi hai, lekin ek half definitely sorted hai. Main us sorted half ki range ko use karke decide karunga ki target wahan reh sakta hai ya nahi."**

Agar target sorted half ke range mein hai:

```text
sorted half possible ✓
other half discard
```

Agar target sorted half ke range mein nahi hai:

```text
sorted half impossible ❌
go to other half
```

Bas.

---

# 15. Common Mistakes

## Mistake 1 — Pehle pivot find karna compulsory samajhna

Pivot separately find kar sakte ho, but zaroori nahi.

Hum directly har iteration mein sorted half detect kar sakte hain.

This keeps the solution clean.

---

## Mistake 2 — Sirf `nums[mid]` ko target se compare karna

Normal Binary Search mein ye enough hota hai.

Yahan nahi.

Because entire array globally sorted nahi hai.

Humein pehle ye jaana hai:

```text
Which half is sorted?
```

Then:

```text
Does target fit inside that sorted range?
```

---

## Mistake 3 — `nums[low] < nums[mid]` blindly use karna

Distinct values ke case mein `<` bhi kai situations mein kaam kar sakta hai, but standard robust form:

```cpp
nums[low] <= nums[mid]
```

Use karo.

---

## Mistake 4 — `mid` ko dobara include karna

Pehle hi:

```cpp
if (nums[mid] == target)
```

check kar chuke.

Isliye range checks mein `mid` ko exclude karna natural hai.

---

## Mistake 5 — Pointer update mein `mid` ko include karna

Agar left jana hai:

```cpp
high = mid - 1;
```

Agar right jana hai:

```cpp
low = mid + 1;
```

Because `mid` already checked.

---

# 16. Final Code

```cpp
class Solution {
public:
    int search(vector<int>& nums, int target) {

        int low = 0;
        int high = nums.size() - 1;

        while (low <= high) {

            int mid = low + (high - low) / 2;

            // Target found
            if (nums[mid] == target) {
                return mid;
            }

            // Left half is sorted
            if (nums[low] <= nums[mid]) {

                // Target lies inside sorted left half
                if (nums[low] <= target && target < nums[mid]) {
                    high = mid - 1;
                }
                else {
                    low = mid + 1;
                }
            }

            // Right half is sorted
            else {

                // Target lies inside sorted right half
                if (nums[mid] < target && target <= nums[high]) {
                    low = mid + 1;
                }
                else {
                    high = mid - 1;
                }
            }
        }

        return -1;
    }
};
```

---

# 17. Code ko line-by-line nahi, thought-by-thought read karo

```cpp
int mid = low + (high - low) / 2;
```

**"Beech ka element dekhte hain."**

```cpp
if (nums[mid] == target)
```

**"Kya answer yahi hai?"**

```cpp
if (nums[low] <= nums[mid])
```

**"Left side sorted hai kya?"**

Then:

```cpp
if (nums[low] <= target && target < nums[mid])
```

**"Agar left sorted hai, toh kya target us sorted range ke andar fit ho raha hai?"**

Yes:

```cpp
high = mid - 1;
```

**"Left possible hai, right hata do."**

No:

```cpp
low = mid + 1;
```

**"Left possible nahi, right try karo."**

Right sorted case mein exactly same thinking reverse direction mein hai.

---

# 18. Complexity

Har iteration mein approximately half search space eliminate hota hai.

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

# 19. Practice — code mat dekho

### Question 1

```text
nums = [5, 6, 7, 8, 1, 2, 3, 4]
target = 2
```

Find:

```text
low = ?
high = ?
mid = ?
nums[mid] = ?

Which half is sorted?

Does target belong to that sorted half?

Where do you move?
```

---

### Question 2

```text
nums = [6, 7, 1, 2, 3, 4, 5]
target = 7
```

Same process.

---

### Question 3

```text
nums = [4, 5, 6, 7, 0, 1, 2]
target = 0
```

Don't immediately write code.

Har iteration mein sirf ye thought follow karo:

```text
Find mid
   ↓
Target mil gaya?
   ↓ NO
Which half is sorted?
   ↓
Target sorted range mein hai?
   ↓
YES → search that half
NO  → search other half
```

The goal is not to memorize the conditions.

The goal is to reach the point where the conditions **feel inevitable** from the reasoning.
