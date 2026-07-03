# Time & Space Complexity (Part 2)

# 16. Space Complexity

Time Complexity tells us **how much time** an algorithm takes.

Space Complexity tells us **how much extra memory** an algorithm uses.

> **Simple Definition**
>
> Space Complexity = Extra memory used by an algorithm as the input size (`n`) grows.

---

### Don't Get Confused

Suppose you already have an array.

```cpp
vector<int> arr = {1,2,3,4,5};
```

This array is **input**, not extra memory.

If you create another array,

```cpp
vector<int> square(5);
```

Now this **counts** in Space Complexity.

---

### Example

```cpp
for(int i=0;i<n;i++)
    square[i]=arr[i]*arr[i];
```

| Memory | Counted? |
|---------|----------|
| Input Array | ❌ No |
| New Array | ✅ Yes |

Extra array size = `n`

Therefore,

```text
Space Complexity = O(n)
```

---

# 17. Auxiliary Space

Interviewers usually ask for

> **Auxiliary Space**

Auxiliary Space = **Extra memory only**

It **doesn't include input memory.**

Example

```cpp
int sum=0;

for(int i=0;i<n;i++)
    sum+=arr[i];
```

Extra variables?

```
sum
i
```

Only constant number of variables.

Therefore

```text
Auxiliary Space = O(1)
```

> **Yaad Rakho**
>
> Space Complexity ≈ Input + Extra Space
>
> Auxiliary Space = Only Extra Space

---

# 18. O(1) — Constant Time

### Idea

No matter how large `n` becomes,

the work remains almost the same.

Example

```cpp
cout<<arr[0];
```

Whether array size is

```
10
```

or

```
10,00,000
```

we directly access index `0`.

Only **one operation**.

Hence

```text
O(1)
```

---

### More Examples

```cpp
arr[n-1]
```

```cpp
top()
```

```cpp
stack.pop()
```

```cpp
queue.front()
```

Most of these take constant time.

---

### Table

| n | Operations |
|---:|-----------:|
|10|1|
|100|1|
|100000|1|

---

> **Interview Tip**
>
> Direct indexing in arrays is almost always **O(1)**.

---

# 19. O(log n) — Logarithmic Time

This is one of the most important complexities.

### Intuition

Imagine finding a word in a dictionary.

Do you start from page 1?

No.

You open somewhere in the middle.

If your word is after that,

ignore the first half.

Again open the middle.

Again throw away half.

Every step removes **half** the search space.

---

### Example

Searching in

```
1024 elements
```

Search space becomes

```
1024

↓

512

↓

256

↓

128

↓

64

↓

32

↓

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

Only **10 steps**!

Not 1024.

---

### Why?

Because

```
2¹⁰ = 1024
```

Hence

```
log₂(1024)=10
```

Therefore

```
O(log n)
```

---

### Real Examples

- Binary Search
- Balanced BST
- Divide Search Space by Half

---

### Comparison

| n | O(n) | O(log n) |
|---:|------:|---------:|
|8|8|3|
|16|16|4|
|32|32|5|
|1024|1024|10|

> **Yaad Rakho**
>
> Whenever you see
>
> **"Search space becomes half"**
>
> immediately think
>
> ```text
> O(log n)
> ```

---

# 20. O(n) — Linear Time

Every element is visited once.

Example

```cpp
for(int i=0;i<n;i++)
```

Loop runs

```
n
```

times.

Hence

```
O(n)
```

---

### Examples

- Linear Search
- Finding Maximum
- Finding Sum
- Counting Frequency

---

### Table

| n | Operations |
|---:|-----------:|
|100|100|
|1000|1000|
|100000|100000|

---

# 21. O(n log n)

Many students get confused here.

Actually,

```
O(n log n)
```

means

```
n work

×

log n levels
```

---

### Merge Sort Intuition

Imagine

```
8 numbers
```

Split

```
8

↓

4 + 4

↓

2 + 2 + 2 + 2

↓

1 + 1 + 1 + ...
```

Splitting happens

```
log n
```

times.

At every level,

all elements are processed once.

```
Work per level = n

Levels = log n

↓

Total = O(n log n)
```

---

### Examples

- Merge Sort
- Heap Sort
- Average Case of Quick Sort

---

### Comparison

| Complexity | Faster? |
|------------|----------|
|O(n)|✅|
|O(n log n)|✅ Good|
|O(n²)|❌ Slower|

---

# 22. O(n²)

Usually comes from

> **Two nested loops**

Example

```cpp
for(...)
{
    for(...)
    {

    }
}
```

Outer loop

```
n
```

Inner loop

```
n
```

Total

```
n × n
```

Hence

```
O(n²)
```

---

### Examples

- Bubble Sort
- Selection Sort
- Insertion Sort (Worst Case)
- Comparing every pair

---

### Example

Finding every pair

```text
(1,2)

(1,3)

(1,4)

...

(n,n)
```

Every element interacts with almost every other element.

---

> **Interview Trick**
>
> Two nested loops **don't always mean** `O(n²)`.
>
> It depends on how the inner loop behaves.

---

# 23. O(n³)

Three nested loops.

```cpp
for(...)
{
    for(...)
    {
        for(...)
        {

        }
    }
}
```

Total work

```
n × n × n
```

↓

```
O(n³)
```

---

### Examples

- Printing all 3D combinations
- Floyd Warshall Algorithm
- Matrix multiplication (basic approach)

---

# 24. O(2ⁿ)

Now things become expensive.

Usually seen in **naive recursion**.

### Example

Fibonacci

```text
F(5)

↓

F(4)+F(3)

↓

F(3)+F(2)+F(2)+F(1)

↓

...
```

Every function creates

```
2 new calls
```

Work doubles repeatedly.

```
1

↓

2

↓

4

↓

8

↓

16
```

Hence

```
O(2ⁿ)
```

---

### Used In

- Recursive Fibonacci
- Backtracking (Brute Force)

---

# 25. O(n!)

Even worse than exponential.

Usually appears when

> We generate **all permutations**.

Example

```
ABC
```

Permutations

```
ABC

ACB

BAC

BCA

CAB

CBA
```

Total

```
3!

=
6
```

If

```
n=10
```

Then

```
10!

=
36,28,800
```

Huge!

---

### Examples

- N Queens (Brute Force)
- Permutations
- Travelling Salesman (Brute Force)

---

# 26. Binary Search Analysis

Why Binary Search is `O(log n)`?

Every iteration

```
Search Space

↓

Half
```

Example

```
64

↓

32

↓

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

Only

```
6
```

iterations.

General Formula

```
n

↓

n/2

↓

n/4

↓

n/8

...

↓

1
```

Hence

```
O(log n)
```

---

# 27. Bubble Sort Analysis

Bubble Sort repeatedly compares adjacent elements.

Example

```
5 4 3 2 1
```

First pass

```
Largest goes to end.
```

Second pass

```
Second largest goes to correct position.
```

...

Number of comparisons

```
n-1

+

n-2

+

...

+

1
```

Which becomes

```
n(n-1)/2
```

Ignoring constants,

```
O(n²)
```

---

# 28. Nested Loop Trick

Don't panic after seeing nested loops.

Check carefully.

Example

```cpp
for(i=0;i<n;i++)
{
    for(j=0;j<5;j++)
    {

    }
}
```

Outer

```
n
```

Inner

```
5
```

Total

```
5n

↓

O(n)
```

Not

```
O(n²)
```

Another example

```cpp
for(i=0;i<n;i++)
{
    for(j=i;j<n;j++)
```

Looks scary.

Still,

```
≈ n²/2

↓

O(n²)
```

---

# 29. Interview Tricks

✔ Ignore constants.

```text
100n

↓

O(n)
```

✔ Ignore smaller terms.

```text
n²+n

↓

O(n²)
```

✔ Think about

> "How does work grow?"

instead of

> "How many lines of code?"

✔ Never calculate using seconds.