# Binary Search — Part 2
## From the Idea to Code, Edge Cases, Complexity & Recursion

Part 1 mein humne Binary Search ka core idea build kiya:

```text
Check middle
    ↓
Compare with target
    ↓
Discard impossible half
    ↓
Continue in remaining half
```

Ab isi thinking ko actual C++ code mein convert karte hain.

---

# 1. `low`, `high`, `mid` Se Code Tak

Suppose:

```cpp
vector<int> arr = {10, 20, 30, 40, 50, 60, 70};
int target = 60;
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
arr[mid] = 40
```

Since:

```text
60 > 40
```

left side impossible.

Therefore:

```cpp
low = mid + 1;
```

This is exactly the logic we learned in Part 1.

---

# 2. The Basic Iterative Code

```cpp
int binarySearch(vector<int>& arr, int target) {
    int low = 0;
    int high = arr.size() - 1;

    while (low <= high) {
        int mid = low + (high - low) / 2;

        if (arr[mid] == target) {
            return mid;
        }
        else if (arr[mid] < target) {
            low = mid + 1;
        }
        else {
            high = mid - 1;
        }
    }

    return -1;
}
```

Ab is code ko ratna nahi hai.

Har line ka reason samjho.

---

# 3. `low = 0`

```cpp
int low = 0;
```

Starting mein poora array search karna hai.

Array ka first valid index:

```text
0
```

So:

```text
low = 0
```

---

# 4. `high = arr.size() - 1`

```cpp
int high = arr.size() - 1;
```

`arr.size()` number of elements deta hai.

For:

```text
[10, 20, 30, 40, 50]
```

size:

```text
5
```

But last index:

```text
4
```

Therefore:

```cpp
high = arr.size() - 1;
```

---

# 5. Why `while (low <= high)`?

This is a very important part.

```cpp
while (low <= high)
```

means:

> Jab tak search karne ke liye at least one valid position available hai, tab tak search karo.

Example:

```text
low = 3
high = 3
```

There is still one element:

```text
index 3
```

So we **must search it**.

That's why:

```text
low <= high
```

is used.

If we wrote:

```cpp
low < high
```

then:

```text
low = high
```

case mein loop stop ho jaata.

That could make us skip the final remaining element.

---

# 6. Why `mid = low + (high - low) / 2`?

We need the middle index.

A common formula is:

```cpp
mid = (low + high) / 2;
```

But safer version:

```cpp
mid = low + (high - low) / 2;
```

Why?

Because theoretically, if `low` and `high` are very large integers, then:

```cpp
low + high
```

can overflow the integer range.

The second formula avoids directly adding the two large values.

So prefer:

```cpp
int mid = low + (high - low) / 2;
```

---

# 7. The Three Decisions in Code

## Case 1 — Target Found

```cpp
if (arr[mid] == target) {
    return mid;
}
```

Simple:

```text
middle == target
      ↓
    FOUND
```

---

## Case 2 — Target Is Bigger

```cpp
else if (arr[mid] < target) {
    low = mid + 1;
}
```

Example:

```text
arr[mid] = 40
target = 60
```

Since:

```text
60 > 40
```

target can only be on the right side.

So:

```cpp
low = mid + 1;
```

---

## Case 3 — Target Is Smaller

```cpp
else {
    high = mid - 1;
}
```

Example:

```text
arr[mid] = 60
target = 30
```

Since:

```text
30 < 60
```

target can only be on the left side.

So:

```cpp
high = mid - 1;
```

---

# 8. Full Dry Run

Array:

```text
[10, 20, 30, 40, 50, 60, 70, 80]
```

Target:

```text
70
```

Indexes:

```text
 0   1   2   3   4   5   6   7
```

### Step 1

```text
low = 0
high = 7
```

```text
mid = 0 + (7 - 0) / 2
mid = 3
```

So:

```text
arr[mid] = 40
```

Target:

```text
70
```

Therefore:

```text
70 > 40
```

Move right:

```text
low = mid + 1
low = 4
```

---

### Step 2

Now:

```text
low = 4
high = 7
```

```text
mid = 4 + (7 - 4) / 2
mid = 5
```

So:

```text
arr[mid] = 60
```

Again:

```text
70 > 60
```

Move right:

```text
low = 6
```

---

### Step 3

Now:

```text
low = 6
high = 7
```

```text
mid = 6 + (7 - 6) / 2
mid = 6
```

So:

```text
arr[mid] = 70
```

Target found.

```text
return 6
```

---

# 9. Important Edge Cases

Binary Search simple hai, but loops mein small mistakes easily ho sakti hain.

Let's deliberately test unusual cases.

---

## Case 1 — Target Is First Element

```text
arr = [10, 20, 30, 40, 50]
target = 10
```

Binary Search ko first element bhi correctly find karna chahiye.

---

## Case 2 — Target Is Last Element

```text
arr = [10, 20, 30, 40, 50]
target = 50
```

Last index:

```text
4
```

Answer:

```text
4
```

---

## Case 3 — Only One Element

```text
arr = [10]
target = 10
```

Initially:

```text
low = 0
high = 0
```

Because:

```text
low <= high
```

loop execute hoga.

```text
mid = 0
```

Target found.

This is one reason `<=` matters.

---

## Case 4 — One Element, Target Doesn't Exist

```text
arr = [10]
target = 20
```

Initially:

```text
low = 0
high = 0
```

Check:

```text
arr[0] = 10
```

Since:

```text
10 < 20
```

we do:

```text
low = mid + 1
low = 1
```

Now:

```text
low = 1
high = 0
```

So:

```text
low > high
```

Search space empty.

Return:

```text
-1
```

---

# 10. Target Smaller Than Everything

```text
arr = [10, 20, 30, 40, 50]
target = 5
```

Target array ke smallest element se bhi chhota hai.

Eventually:

```text
high < low
```

and search stops.

Answer:

```text
-1
```

---

# 11. Target Larger Than Everything

```text
arr = [10, 20, 30, 40, 50]
target = 100
```

Every time target middle se bigger hoga.

So:

```text
low = mid + 1
```

move hota rahega.

Eventually:

```text
low > high
```

and:

```text
-1
```

return hoga.

---

# 12. Empty Array

Agar array empty ho:

```cpp
vector<int> arr;
```

then:

```cpp
arr.size() = 0
```

and:

```cpp
high = arr.size() - 1;
```

needs care because `size()` is unsigned.

In practical interview/LeetCode code, a clean approach is often to handle empty input first or use an appropriate integer conversion.

For example:

```cpp
if (arr.empty()) {
    return -1;
}
```

Then normal Binary Search start kar sakte ho.

The important lesson:

> Input constraints and data types ko ignore mat karo.

---

# 13. Duplicate Values

Suppose:

```text
arr = [10, 20, 20, 20, 30]
target = 20
```

Basic Binary Search ka kaam hai:

> target ka **koi valid index** find karna.

It does not automatically guarantee:

```text
first occurrence
```

or:

```text
last occurrence
```

Those are different problems.

Later hum same Binary Search idea ko modify karke:

- first occurrence
- last occurrence
- lower bound
- upper bound

find karenge.

---

# 14. Time Complexity — Why `O(log n)`?

This should not be a formula to memorize.

Binary Search mein search space half hota hai.

Suppose:

```text
n = 16
```

Then:

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

Suppose number of steps = `k`.

After `k` divisions:

```text
n / 2^k = 1
```

So:

```text
n = 2^k
```

Therefore:

```text
k = log₂ n
```

Hence:

```text
Time Complexity = O(log n)
```

---

# 15. Linear Search vs Binary Search

For:

```text
n = 1,000,000
```

Linear Search:

```text
O(n)
```

could require around:

```text
1,000,000
```

checks in the worst case.

Binary Search:

```text
O(log n)
```

needs roughly:

```text
log₂(1,000,000) ≈ 20
```

checks.

That's the real reason Binary Search is powerful.

Not because the code is small.

Because **each comparison throws away a huge part of the remaining search space.**

---

# 16. Space Complexity

Our iterative code uses only:

```text
low
high
mid
```

These are just a few variables.

Array ke size ke saath extra memory grow nahi hoti.

Therefore:

```text
Space Complexity = O(1)
```

---

# 17. Recursive Binary Search

Binary Search ko recursion se bhi implement kar sakte hain.

Thinking:

```text
Search current range
        ↓
Check middle
        ↓
Target left?
   → Search left range again

Target right?
   → Search right range again
```

For example:

```text
binarySearch(arr, target, low, high)
```

function ko current search range diya jaata hai.

---

# 18. Recursive Base Case

Sabse important question:

> Kab stop karna hai?

Agar:

```text
low > high
```

then search space empty hai.

So:

```cpp
if (low > high) {
    return -1;
}
```

Second stopping condition:

```cpp
if (arr[mid] == target) {
    return mid;
}
```

Target mil gaya.

---

# 19. Recursive Code

```cpp
int binarySearch(vector<int>& arr, int target, int low, int high) {
    if (low > high) {
        return -1;
    }

    int mid = low + (high - low) / 2;

    if (arr[mid] == target) {
        return mid;
    }

    if (arr[mid] < target) {
        return binarySearch(arr, target, mid + 1, high);
    }

    return binarySearch(arr, target, low, mid - 1);
}
```

Same logic hai.

Difference sirf itna hai ki iterative version mein:

```cpp
while
```

use hua tha.

Recursive version mein:

```cpp
function calls itself
```

---

# 20. Recursive Dry Run

Array:

```text
[10, 20, 30, 40, 50, 60, 70]
```

Target:

```text
60
```

First call:

```text
low = 0
high = 6
```

Middle:

```text
mid = 3
arr[mid] = 40
```

Since:

```text
60 > 40
```

call:

```text
binarySearch(arr, 60, 4, 6)
```

Now:

```text
low = 4
high = 6
```

Middle:

```text
mid = 5
arr[mid] = 60
```

Found.

Return:

```text
5
```

Notice the search logic exactly same hai.

---

# 21. Iterative vs Recursive

### Iterative

Uses:

```cpp
while
```

Extra space:

```text
O(1)
```

### Recursive

Uses function call stack.

Each recursive call stays on the call stack until it returns.

Maximum recursion depth:

```text
O(log n)
```

So auxiliary space:

```text
O(log n)
```

For Binary Search, iterative implementation is usually preferable when we only care about keeping extra space constant.

---

# 22. The Real Pattern to Remember

Binary Search ko sirf is form mein mat yaad karo:

```cpp
low = 0;
high = n - 1;
```

Real thinking:

```text
1. What is my current search space?
2. What is the middle?
3. What information does the middle give me?
4. Which half is impossible?
5. How do I remove that half?
6. When does my search space become empty?
```

Agar ye six questions clear hain, toh code naturally aa jayega.

---

# Practice

Ab bina code dekhe manually solve karo:

```text
arr = [2, 5, 8, 12, 16, 21, 27, 35, 42, 50]
target = 21
```

Track:

```text
Step 1:
low = ?
high = ?
mid = ?
arr[mid] = ?

Which half gets eliminated?

Step 2:
low = ?
high = ?
mid = ?
arr[mid] = ?

Step 3:
...
```

Then try these mentally:

```text
1. target = 2
2. target = 50
3. target = 17
4. arr = [10], target = 10
5. arr = [10], target = 20
```

For each one, don't start with code.

First decide:

> **Middle kya hai, target kis side ho sakta hai, aur kaunsa half throw away kar sakta hoon?**

Once this becomes natural, Binary Search ke next problems mein hum isi idea ko modify karke more interesting patterns solve karenge.
