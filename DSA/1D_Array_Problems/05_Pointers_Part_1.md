# C++ Pointers — Part 1

## 1. Normal Variable

```cpp
int a = 5;
```

This means:

- `a` is an integer variable.
- `5` is the value stored in `a`.
- `a` is stored somewhere in memory.
- That location has a **memory address**.

For understanding, assume:

```text
Address    Value
1000       5
```

So:

```text
a → 5
```

and:

```text
&a → address of a
```

`&` means: **"give me the address of this variable."**

---

## 2. Why Do We Need Pointers?

Normally:

```cpp
cout << a;
```

gives:

```text
5
```

But sometimes we don't want the value directly. We want to work with the **memory location** where that value is stored.

That's where pointers come in.

A pointer is a variable whose job is to **store an address**.

---

## 3. Creating a Pointer

```cpp
int *p = &a;
```

Break it into two parts:

```text
int *p
```

means:

> `p` is a pointer that points to an `int`.

And:

```text
&a
```

means:

> address of `a`.

So:

```cpp
int *p = &a;
```

means:

> Store the address of `a` inside `p`.

Suppose `a` is at address `1000`:

```text
a
Address: 1000
Value:   5

p
Address: 2000
Value:   1000
```

Notice the important difference:

```text
a → 5
p → address of a
```

`p` does **not** contain `5`.

It contains the address where `5` is stored.

---

## 4. What Does `*p` Mean?

Now:

```cpp
*p
```

means:

> Go to the address stored inside `p` and access the value there.

Since:

```text
p → address of a
```

therefore:

```text
*p → value of a
   → 5
```

So:

```cpp
cout << p;
```

prints the address stored in `p`.

While:

```cpp
cout << *p;
```

prints the value at that address.

The key difference:

```text
p
↓
address

*p
↓
value at that address
```

---

## 5. Pointer to a Pointer

Now consider:

```cpp
int **q = &p;
```

Again, don't look at `**` as something magical.

We already know:

```cpp
int *p = &a;
```

So `p` is a variable.

And just like every normal variable, `p` itself also has a memory address.

Therefore:

```cpp
&p
```

means:

> address of `p`.

So:

```cpp
int **q = &p;
```

means:

> `q` stores the address of `p`.

The chain becomes:

```text
q → p → a → 5
```

More precisely:

```text
q
│
│ stores address of p
▼
p
│
│ stores address of a
▼
a
│
│ stores 5
▼
5
```

This is called a **pointer to a pointer**.

---

## 6. What Does `*q` Mean?

Remember:

```text
q → address of p
```

Therefore:

```cpp
*q
```

means:

> Go to the address stored in `q` and access what is stored there.

At that location we find `p`.

So:

```text
*q → p
```

And since `p` contains the address of `a`:

```text
*q
```

has the same value as:

```text
p
```

So both represent the **address of `a`**.

---

## 7. What Does `**q` Mean?

Now apply `*` one more time.

First:

```text
*q
```

gives:

```text
p
```

Then:

```text
**q
```

means:

```text
*(*q)
```

Since:

```text
*q → p
```

we get:

```text
*(*q)
= *p
= 5
```

Therefore:

```text
**q → 5
```

The complete chain:

```text
q
↓
p
↓
a
↓
5
```

So:

```text
q    → address of p
*q   → address of a
**q  → 5
```

---

## 8. Complete Example

```cpp
int a = 5;

int *p = &a;

int **q = &p;

cout << *p << endl;
cout << **q << endl;
cout << p << endl;
cout << *q << endl;
```

Let's understand each statement.

### `*p`

`p` contains the address of `a`.

Therefore:

```text
*p → value of a → 5
```

Output:

```text
5
```

### `**q`

First:

```text
*q → p
```

Then:

```text
**q → *p → 5
```

Output:

```text
5
```

### `p`

`p` stores the address of `a`.

So:

```cpp
cout << p;
```

prints the address of `a`.

It may look something like:

```text
0x61ff08
```

The exact address is not fixed.

### `*q`

`q` stores the address of `p`.

Therefore:

```text
*q → p
```

And `p` stores the address of `a`.

So:

```text
*q
```

prints the same address represented by `p`.

---

## 9. Complete Memory Picture

Assume:

```text
a is at address 1000
p is at address 2000
q is at address 3000
```

Then:

```text
Variable    Address    Stored Value

a           1000          5

p           2000         1000
                         ↑
                    address of a

q           3000         2000
                         ↑
                    address of p
```

Visual:

```text
q
│
│ contains 2000
▼
p
│
│ contains 1000
▼
a
│
│ contains 5
▼
5
```

Therefore:

```text
p    → 1000
*p   → 5

q    → 2000
*q   → 1000
**q  → 5
```

---

## 10. `&` and `*`

A useful way to remember them:

### `&`

```cpp
&a
```

means:

> Give me the address of `a`.

So:

```text
variable → address
```

### `*`

```cpp
*p
```

means:

> Go to the address stored in `p` and give me the value there.

So:

```text
address → value
```

Example:

```cpp
int a = 5;
int *p = &a;
```

Then:

```text
&a → address of a
p  → address of a
*p → 5
```

---

## 11. Why `int *` and `int **`?

The type tells us what the pointer is pointing to.

```cpp
int *p;
```

means:

```text
p → pointer to an int
```

And:

```cpp
int **q;
```

means:

```text
q → pointer to a pointer to an int
```

Because:

```text
q → p → int
```

So:

```text
int
int *
int **
int ***
```

represent increasing levels of indirection.

For now, focus strongly on:

```text
int *   → pointer
int **  → pointer to pointer
```

---

## 12. Pointers Can Also Modify the Original Variable

Pointers are not only for reading values.

Example:

```cpp
int a = 5;

int *p = &a;

*p = 10;
```

What happened?

`p` points to `a`.

So:

```cpp
*p
```

means:

> The actual variable `a`.

Therefore:

```cpp
*p = 10;
```

changes `a`.

Before:

```text
a = 5
```

After:

```text
a = 10
```

Visual:

```text
p ───────→ a
           │
           ▼
          10
```

This is one of the most important reasons pointers are useful: **we can access and modify another variable through its address.**

---

## 13. Quick Reference

| Expression | Meaning |
|---|---|
| `a` | value of `a` |
| `&a` | address of `a` |
| `p` | address stored in `p` |
| `*p` | value at the address stored in `p` |
| `&p` | address of pointer `p` |
| `q` | address stored in `q` |
| `*q` | value stored at `q`'s address → `p` |
| `**q` | value reached through `q` → `a`'s value |

For:

```cpp
int a = 5;
int *p = &a;
int **q = &p;
```

remember:

```text
q → p → a → 5
```

---

## Practice

Without running this code, predict all three outputs:

```cpp
int a = 10;

int *p = &a;

int **q = &p;

*p = 20;

cout << a << endl;
cout << *p << endl;
cout << **q << endl;
```

Don't just memorize it.

Trace the chain:

```text
q → p → a
```

and determine what changed after:

```cpp
*p = 20;
```

Then answer:

> What will you build with pointers?
