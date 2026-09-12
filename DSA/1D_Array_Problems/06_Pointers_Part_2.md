# C++ Pointers — Part 2
## Pointers with Arrays

Part 1 mein humne dekha tha:

```text
pointer → variable → value
```

Ab pointer ko array ke saath connect karte hain.

---

## 1. Array Ko Samjho

```cpp
int arr[] = {10, 20, 30, 40};
```

Array memory mein elements ko one after another store karta hai.

```text
Index:     0      1      2      3

          ┌────┬────┬────┬────┐
arr  →    │ 10 │ 20 │ 30 │ 40 │
          └────┴────┴────┴────┘
```

For example, conceptually addresses ho sakte hain:

```text
arr[0] → 1000
arr[1] → 1004
arr[2] → 1008
arr[3] → 1012
```

Exact addresses different honge. Important point hai ki array elements **contiguous** hote hain, yani memory mein paas-paas stored hote hain.

---

# 2. `int *ptr = arr;`

Ab:

```cpp
int *ptr = arr;
```

Yahan `arr` ko first element ke address ki tarah use kiya ja raha hai.

So:

```text
arr
 ↓
address of arr[0]
```

Therefore:

```text
ptr → arr[0]
```

Visual:

```text
ptr
 ↓
┌────┬────┬────┬────┐
│ 10 │ 20 │ 30 │ 40 │
└────┴────┴────┴────┘
  ↑
arr[0]
```

So:

```cpp
*ptr
```

gives:

```text
10
```

because `ptr` points to `arr[0]`.

---

# 3. Pointer Arithmetic

Ab important part:

```cpp
*(ptr + 1)
```

Isko ek saath mat dekho. Step by step dekho.

### Step 1

Initially:

```text
ptr → arr[0]
```

### Step 2

```cpp
ptr + 1
```

means:

> Next `int` position par move karo.

So:

```text
ptr       → arr[0]
ptr + 1   → arr[1]
```

### Step 3

Now:

```cpp
*(ptr + 1)
```

means:

> Us position par jo value hai, woh do.

Therefore:

```text
*(ptr + 1)
= arr[1]
= 20
```

So:

```cpp
cout << *(ptr + 1);
```

prints:

```text
20
```

---

# 4. `*(ptr + 3)`

Same idea:

```cpp
*(ptr + 3)
```

Start:

```text
ptr → arr[0]
```

Move three positions:

```text
ptr       → arr[0]
ptr + 1   → arr[1]
ptr + 2   → arr[2]
ptr + 3   → arr[3]
```

Then dereference:

```text
*(ptr + 3)
= arr[3]
= 40
```

So output:

```text
40
```

---

# 5. Most Important Relationship

If:

```cpp
int *ptr = arr;
```

then:

```cpp
*(ptr + i)
```

gives the same element as:

```cpp
arr[i]
```

For example:

```text
*(ptr + 0) → 10
*(ptr + 1) → 20
*(ptr + 2) → 30
*(ptr + 3) → 40
```

So remember:

```text
*(ptr + i)  ≈  arr[i]
```

Ye pointer + array ka core idea hai.

---

# 6. `ptr + 1` Address Mein Sirf 1 Add Nahi Karta

Ek common confusion:

Suppose:

```text
ptr = 1000
```

Kya:

```text
ptr + 1 = 1001
```

?

**Nahi.**

Pointer arithmetic type ke according hoti hai.

Here:

```cpp
int *ptr;
```

So `ptr + 1` means:

> Move to the next `int`.

If one `int` takes 4 bytes, conceptually:

```text
ptr       = 1000
ptr + 1   = 1004
ptr + 2   = 1008
ptr + 3   = 1012
```

C++ automatically correct amount move karta hai.

Isliye tumhe manually `4` bytes add karne ki need nahi hoti.

---

# 7. Ab `ptr++`

Code:

```cpp
ptr++;
```

Iska meaning:

> Pointer ko next element par move karo.

Initially:

```text
ptr → arr[0]
```

After:

```cpp
ptr++;
```

now:

```text
ptr → arr[1]
```

Visual:

### Before

```text
ptr
 ↓
┌────┬────┬────┬────┐
│ 10 │ 20 │ 30 │ 40 │
└────┴────┴────┴────┘
```

### After `ptr++`

```text
     ptr
      ↓
┌────┬────┬────┬────┐
│ 10 │ 20 │ 30 │ 40 │
└────┴────┴────┴────┘
```

Now:

```cpp
*ptr
```

gives:

```text
20
```

---

# 8. `ptr + 1` vs `ptr++`

Dono similar lag sakte hain, but difference important hai.

### `ptr + 1`

```cpp
*(ptr + 1)
```

means:

> `ptr` se next position dekho.

`ptr` khud move nahi hota.

Example:

```cpp
int *ptr = arr;

cout << *(ptr + 1) << endl;
cout << *ptr << endl;
```

Output:

```text
20
10
```

Because `ptr` still `arr[0]` ko point kar raha hai.

---

### `ptr++`

```cpp
ptr++;
```

means:

> `ptr` ko actually next position par move karo.

So:

```cpp
int *ptr = arr;

ptr++;

cout << *ptr << endl;
```

Output:

```text
20
```

Now `ptr` itself `arr[1]` ko point kar raha hai.

---

# 9. Complete Code Dry Run

```cpp
int arr[] = {10, 20, 30, 40};

int *ptr = arr;

cout << *(ptr + 1) << endl;
cout << *(ptr + 3) << endl;

ptr++;

cout << *ptr << endl;
```

## Starting Point

```text
ptr → arr[0]
```

---

## First Print

```cpp
*(ptr + 1)
```

Move one position:

```text
ptr + 1 → arr[1]
```

Value:

```text
20
```

Output:

```text
20
```

Important: `ptr` itself abhi bhi `arr[0]` ko point kar raha hai.

---

## Second Print

```cpp
*(ptr + 3)
```

Move three positions:

```text
ptr + 3 → arr[3]
```

Value:

```text
40
```

Output:

```text
40
```

Again, `ptr` itself change nahi hua.

---

## `ptr++`

Initially:

```text
ptr → arr[0]
```

After:

```cpp
ptr++;
```

we get:

```text
ptr → arr[1]
```

---

## Last Print

```cpp
*ptr
```

Since:

```text
ptr → arr[1]
```

therefore:

```text
*ptr = 20
```

Final output:

```text
20
40
20
```

---

# 10. Array Indexing Aur Pointer Arithmetic

Ek aur important connection:

```cpp
arr[i]
```

and:

```cpp
*(arr + i)
```

same element ko access karte hain.

Example:

```cpp
arr[2]
```

is equivalent to:

```cpp
*(arr + 2)
```

And because:

```cpp
int *ptr = arr;
```

we can also write:

```cpp
*(ptr + 2)
```

So:

```text
arr[2]
   ↓
*(arr + 2)
   ↓
*(ptr + 2)
   ↓
30
```

This is why pointer arithmetic and arrays are closely connected.

---

# 11. Why Does This Matter in DSA?

Abhi ye sirf ek syntax trick mat samjho.

Underlying idea ye hai:

> Pointer ek position ko remember kar sakta hai, aur pointer arithmetic se hum consecutive elements ke beech move kar sakte hain.

Array:

```text
[10] [20] [30] [40]
  ↑
 pointer
```

Move:

```text
ptr++
```

Then:

```text
[10] [20] [30] [40]
       ↑
     pointer
```

Again:

```text
ptr++
```

Then:

```text
[10] [20] [30] [40]
             ↑
           pointer
```

Ye basic movement idea later DSA mein bahut baar dikhega.

---

# 12. Array Ke Bahar Mat Jaana

Given:

```cpp
int arr[] = {10, 20, 30, 40};
```

Valid indexes:

```text
0
1
2
3
```

So:

```cpp
*(ptr + 0)
*(ptr + 1)
*(ptr + 2)
*(ptr + 3)
```

valid elements ko access karte hain.

But:

```cpp
*(ptr + 4)
```

array ke bahar dereference karega.

Isliye valid range ka dhyan rakhna important hai.

---

# Practice

Without running the code, output predict karo:

```cpp
int arr[] = {5, 15, 25, 35, 45};

int *ptr = arr;

cout << *ptr << endl;

ptr++;

cout << *ptr << endl;

cout << *(ptr + 2) << endl;

ptr++;

cout << *ptr << endl;
```

Pehle pointer ki position track karo:

```text
Initially:
ptr → ?

After first ptr++:
ptr → ?

After second ptr++:
ptr → ?
```

Then har expression ka value nikalo.

