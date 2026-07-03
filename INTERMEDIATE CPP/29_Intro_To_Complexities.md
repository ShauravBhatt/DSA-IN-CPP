# Time & Space Complexity (Part 1)

# 1. Why Time Complexity Exists?

Suppose two students solve the same problem.

| Student A | Student B |
|-----------|-----------|
| Correct Answer | Correct Answer |
| Runs in 2 sec | Runs in 0.01 sec |

Question:

> **Which solution is better?**

Correctness alone isn't enough. We also care about **efficiency**.

Time Complexity helps us:

- Compare algorithms
- Choose better solutions
- Optimize brute-force code
- Answer interview questions

> **Remember:** Programming is not only about *making code work*, but also about *making it work efficiently*.

---

# 2. Actual Time ≠ Time Complexity

Many beginners think:

```text
Time Complexity = Execution Time
```

❌ Wrong.

Execution time depends on hardware.

| Depends On | Example |
|------------|----------|
| CPU | i3 vs i9 |
| RAM | 8 GB vs 32 GB |
| Compiler | GCC vs Clang |
| OS | Windows vs Linux |

So,

Same code →

```text
Windows → 0.40 sec
Linux → 0.22 sec
Mac → 0.18 sec
```

Time changes.

But

```
Time Complexity
```

never changes.

### Idea

Instead of measuring **seconds**, Computer Science measures

```text
Input Size (n) → Number of Operations
```

---

# 3. Machine Independence

Time Complexity is **machine-independent**.

Whether your code runs on

- Laptop
- PC
- Server
- Supercomputer

the complexity remains the same.

Because we measure

> **Growth of work**, not execution time.

---

# 4. What is an Operation?

Operation = Any small instruction executed by CPU.

Examples

```cpp
int x = 5;
```

```cpp
sum += arr[i];
```

```cpp
i++;
```

```cpp
if(a>b)
```

Each is approximately **one operation**.

If a loop runs 100 times,

then roughly

```
100 operations
```

are performed.

> **Yaad Rakho:** Time Complexity ultimately counts **operations**, not seconds.

---

# 5. Input Size (n)

`n` simply means

> **Size of the input.**

Examples

| Problem | Meaning of n |
|----------|--------------|
| Array | Number of elements |
| String | Length |
| Linked List | Number of nodes |
| Matrix | Number of rows/columns |

Example

```cpp
vector<int> arr(100);
```

```
n = 100
```

Simple as that.

---

# 6. What is Time Complexity?

**Definition**

> Time Complexity tells us **how the number of operations grows as input size grows.**

Think like this:

```text
n increases → Operations increase → Complexity changes
```

Notice

We are **not measuring time**.

We are measuring

```
Work Done
```

---

# 7. Linear Search Intuition

Suppose

```text
[2, 5, 8, 1, 7]
```

Searching

```
7
```

Linear Search checks one-by-one.

```text
2 → 5 → 8 → 1 → 7
```

If

| n | Maximum Checks |
|---|---------------:|
|5|5|
|100|100|
|1000|1000|

Pattern

```
Operations grow exactly like n.
```

Hence

```text
O(n)
```

> **Interview Tip:** Worst case occurs when the target is at the last index or doesn't exist.

---

# 8. Graph Intuition (Without Graph 😄)

Instead of drawing graphs, observe the relation.

| Input Size (n) | Operations |
|---------------:|-----------:|
|1|1|
|10|10|
|100|100|
|1000|1000|

Notice

```text
n doubles → Operations also double
```

This is called **Linear Growth**.

Hence

```text
f(n) = n

↓

O(n)
```

---

# 9. Big O Notation

Big O is **not the algorithm**.

It is simply a notation used to describe an algorithm's growth.

Examples

```text
O(1)

O(log n)

O(n)

O(n²)
```

Think of it like a symbol.

| Symbol | Represents |
|---------|------------|
| ₹ | Rupee |
| $ | Dollar |
| O() | Time Complexity |

---

# 10. Why Worst Case?

Whenever we calculate Time Complexity,

we usually calculate

> **Worst Case Complexity.**

Why?

Because interviews and real systems care about

> "Maximum time your algorithm can take."

Example

Searching

```text
[1 2 3 4 5]
```

Searching

```
5
```

Need to check all elements.

Worst Case

```
n operations
```

Searching

```
1
```

Best Case

```
1 operation
```

Unless mentioned,

always assume

```
Worst Case
```

---

# 11. Upper Bound

Big O represents

> **Upper Bound**

Meaning

Algorithm will take

**at most**

that much work.

Example

Linear Search

Maximum possible checks

```
n
```

Hence

```
O(n)
```

It can perform better,

but never worse than this bound.

---

# 12. Rules to Calculate Big O

Almost every question follows these two rules.

### Rule 1

Ignore constants.

### Rule 2

Keep only the largest-growing term.

That's all.

---

# 13. Ignore Constants

Example

```text
4n² + 3n + 5
```

Step 1

Ignore constants

```text
n² + n + 1
```

Step 2

Among

```text
n²

n

1
```

Largest is

```text
n²
```

Final

```text
O(n²)
```

Another Example

```text
100 + 5n + 20
```

↓

```text
n
```

↓

```text
O(n)
```

> **Yaad Rakho:** Numbers don't matter. Growth matters.

---

# 14. Dominant Term

For very large `n`, the fastest-growing term dominates.

Examples

| Function | Final Big O |
|----------|-------------|
| n + 5 | O(n) |
| n² + n | O(n²) |
| n³ + n² + n | O(n³) |
| n log n + n | O(n log n) |
| log n + n² | O(n²) |

Example

Suppose

```
n = 1,000,000
```

Then

```
n²
```

is enormously larger than

```
n
```

So we ignore smaller terms.

---

# 15. Big O vs Theta vs Omega

There are three important notations.

| Notation | Meaning | Represents |
|----------|----------|------------|
| **O()** | Upper Bound | Worst Case |
| **Θ()** | Tight Bound | Exact Growth |
| **Ω()** | Lower Bound | Best Case |

Example: Linear Search

| Case | Complexity |
|------|------------|
| Target at first index | Ω(1) |
| Typical behaviour | Θ(n) |
| Target at last index | O(n) |

### Placement Point of View

In almost every coding interview,

you'll mostly calculate

```text
Big O
```

Theta and Omega are mainly useful in theoretical Computer Science and university exams.

---

# Quick Revision

| Concept | Remember |
|----------|----------|
| Time Complexity | Growth of operations |
| Execution Time | Machine-dependent |
| Time Complexity | Machine-independent |
| Input Size | Represented by `n` |
| Big O | Worst Case |
| Ignore | Constants |
| Keep | Largest term |
| O() | Upper Bound |
| Θ() | Tight Bound |
| Ω() | Lower Bound |
