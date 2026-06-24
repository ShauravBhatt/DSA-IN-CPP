# Bitwise Operations – Hinglish + English Notes

## 1. What is a Bit?

A **Bit (Binary Digit)** is the smallest unit of data in a computer.

A bit can store only two values:

```text
0
1
```

Computer ke andar jo bhi data hota hai (numbers, characters, images, videos), sab ultimately bits ki form mein store hota hai.

### Examples

```text
Decimal 5  = 0101
Decimal 7  = 0111
Decimal 10 = 1010
```

---

# 2. Binary Number System

Hum normally **Decimal System (Base-10)** use karte hain:

```text
0,1,2,3,4,5,6,7,8,9
```

Lekin computer **Binary System (Base-2)** use karta hai:

```text
0,1
```

### Place Values in Binary

```text
Binary : 1 0 1 1
Position: 3 2 1 0
```

Calculation:

```text
1×2³ + 0×2² + 1×2¹ + 1×2⁰

= 8 + 0 + 2 + 1
= 11
```

Therefore:

```text
1011₂ = 11₁₀
```

### Easy Memory Trick

Decimal mein:

```text
1,10,100,1000
```

powers of 10 hote hain.

Binary mein:

```text
1,2,4,8,16,32,64...
```

powers of 2 hote hain.

---

# 3. What are Bitwise Operations?

Bitwise operations numbers ke **individual bits** par kaam karti hain.

Normal arithmetic:

```cpp
5 + 3 = 8
```

Bitwise operations:

```text
5 = 0101
3 = 0011
```

Har bit ko separately compare kiya jata hai.

### Why Learn Bitwise?

Used in:

- Competitive Programming
- DSA
- Operating Systems
- Networking
- Embedded Systems
- Cryptography
- Game Development

---

# 4. Bitwise AND (`&`)

## Rule

Result tabhi `1` aayega jab **dono bits 1 ho.**

| A | B | A & B |
|---|---|---|
| 0 | 0 | 0 |
| 0 | 1 | 0 |
| 1 | 0 | 0 |
| 1 | 1 | 1 |

### Example

```text
5 = 0101
3 = 0011
------------
& = 0001
```

Answer:

```text
1
```

### Visual Understanding

```text
0 & 0 = 0
0 & 1 = 0
1 & 0 = 0
1 & 1 = 1
```

AND bahut strict hai.

"Sabko permission milegi tabhi pass karunga."

### Important Use

Odd/Even Check

```cpp
n & 1
```

Example:

```text
7 = 0111

0111
0001
----
0001
```

Result ≠ 0

So:

```text
7 is Odd
```

---

# 5. Bitwise OR (`|`)

## Rule

Agar kisi bhi bit par `1` ho to result `1`.

| A | B | A \| B |
|---|---|---|
| 0 | 0 | 0 |
| 0 | 1 | 1 |
| 1 | 0 | 1 |
| 1 | 1 | 1 |

### Example

```text
5 = 0101
3 = 0011
------------
| = 0111
```

Answer:

```text
7
```

### Visual Understanding

OR bahut generous hai.

"Ek bhi banda yes bol de to approve."

```text
0 | 0 = 0
0 | 1 = 1
1 | 0 = 1
1 | 1 = 1
```

### Use

Specific bit ko ON (1) karne ke liye.

---

# 6. Bitwise XOR (`^`)

## Rule

Bits different hon to `1`.

Bits same hon to `0`.

| A | B | A ^ B |
|---|---|---|
| 0 | 0 | 0 |
| 0 | 1 | 1 |
| 1 | 0 | 1 |
| 1 | 1 | 0 |

### Example

```text
5 = 0101
3 = 0011
------------
^ = 0110
```

Answer:

```text
6
```

---

## XOR Memory Trick

XOR ka matlab:

```text
Different = 1
Same      = 0
```

### Example

```text
1 ^ 1 = 0
0 ^ 0 = 0

1 ^ 0 = 1
0 ^ 1 = 1
```

---

## Important XOR Properties

### Property 1

```cpp
A ^ A = 0
```

Example:

```cpp
5 ^ 5 = 0
```

Kyun?

Har bit same hai.

---

### Property 2

```cpp
A ^ 0 = A
```

Example:

```cpp
7 ^ 0 = 7
```

---

### Property 3

```cpp
A ^ B ^ B = A
```

Because:

```cpp
B ^ B = 0
```

Ye property CP aur interviews mein bahut use hoti hai.

---

# 7. Bitwise NOT (`~`)

NOT operator har bit ko reverse kar deta hai.

```text
0 → 1
1 → 0
```

### Example

```text
5 = 00000101

~5 = 11111010
```

---

## Difficult Concept: Why ~5 = -6 ?

Ye beginners ko confuse karta hai.

### Step 1

```text
5 = 00000101
```

NOT lagaya:

```text
11111010
```

Computer negative numbers ko store karta hai using:

```text
Two's Complement
```

### Shortcut Formula

```cpp
~n = -(n + 1)
```

Example:

```cpp
~5

= -(5+1)

= -6
```

### Interview Fact

```cpp
~10 = -11
~7  = -8
~0  = -1
```

Ye formula yaad rakhna.

---

# 8. Left Shift (`<<`)

Bits ko left side move karta hai.

### Formula

```text
A << B = A × 2ᴮ
```

### Example

```text
5 = 0101

5 << 1

0101 → 1010
```

Result:

```text
10
```

---

### Example 2

```text
5 << 2
```

Means:

```text
5 × 2²

5 × 4

20
```

---

## Easy Memory

```cpp
n << 1 = n × 2
n << 2 = n × 4
n << 3 = n × 8
```

Har left shift number ko double karta hai.

---

# 9. Right Shift (`>>`)

Bits ko right side move karta hai.

### Formula

(Positive numbers ke liye)

```text
A >> B = A / 2ᴮ
```

---

### Example

```text
8 = 1000

8 >> 1

1000 → 0100
```

Result:

```text
4
```

---

### Example

```text
16 >> 2
```

Means:

```text
16 / 4

= 4
```

---

## Easy Memory

```cpp
n >> 1 = n / 2
n >> 2 = n / 4
n >> 3 = n / 8
```

---

# 10. Most Important Bit Tricks

## Check Odd or Even

```cpp
if(n & 1)
```

Reason:

Even numbers:

```text
6 = 0110
```

Last bit:

```text
0
```

Odd numbers:

```text
7 = 0111
```

Last bit:

```text
1
```

Therefore:

```cpp
n & 1
```

directly odd/even bata deta hai.

---

## Multiply by 2

```cpp
n << 1
```

Example:

```cpp
8 << 1 = 16
```

---

## Divide by 2

```cpp
n >> 1
```

Example:

```cpp
16 >> 1 = 8
```

---

## Check Power of 2

### Formula

```cpp
n > 0 && (n & (n-1)) == 0
```

### Why It Works?

Take:

```text
8 = 1000
```

```text
7 = 0111
```

AND:

```text
1000
0111
----
0000
```

Result becomes 0.

Power of 2 numbers always have exactly one set bit.

Examples:

```text
1  = 0001
2  = 0010
4  = 0100
8  = 1000
16 =10000
```

---

# Quick Revision Sheet

| Operator | Name | Meaning |
|-----------|--------|---------|
| `&` | AND | Both bits must be 1 |
| `\|` | OR | At least one bit is 1 |
| `^` | XOR | Different bits → 1 |
| `~` | NOT | Reverse all bits |
| `<<` | Left Shift | Multiply by 2^k |
| `>>` | Right Shift | Divide by 2^k |