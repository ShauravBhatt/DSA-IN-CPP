# Binary Number System Notes

# 1. Intuition Behind Binary Number System

Hum daily life me Decimal Number System use karte hain.

```text
Digits:
0 1 2 3 4 5 6 7 8 9
```

Isko Base-10 System kehte hain.

Reason:

```text
10 symbols available
```

---

Computer ke paas sirf do electrical states hoti hain:

```text
HIGH Voltage
LOW Voltage
```

Isliye computer naturally represent karta hai:

```text
HIGH -> 1
LOW  -> 0
```

Aur isi wajah se computer Binary Number System use karta hai.

```text
Base = 2
Digits = 0, 1
```

---

# Decimal Place Values

Decimal me:

```text
538
```

Actually hota hai:

```text
5 × 10² +
3 × 10¹ +
8 × 10⁰
```

```text
500 + 30 + 8
```

---

# Binary Place Values

Binary me:

```text
10110
```

Actually hota hai:

```text
1 × 2⁴ +
0 × 2³ +
1 × 2² +
1 × 2¹ +
0 × 2⁰
```

```text
16 + 0 + 4 + 2 + 0
```

```text
= 22
```

---

# 2. Decimal to Binary Conversion

## Core Idea

Har step par:

```text
Divide by 2
Store Remainder
```

Final Binary:

```text
Bottom to Top
```

---

# Example 1

Convert:

```text
13
```

| Division | Quotient | Remainder |
| -------- | -------- | --------- |
| 13 ÷ 2   | 6        | 1         |
| 6 ÷ 2    | 3        | 0         |
| 3 ÷ 2    | 1        | 1         |
| 1 ÷ 2    | 0        | 1         |

Read bottom to top:

```text
1101
```

Therefore:

```text
13 = 1101₂
```

---

# Example 2

Convert:

```text
25
```

| Division | Quotient | Remainder |
| -------- | -------- | --------- |
| 25 ÷ 2   | 12       | 1         |
| 12 ÷ 2   | 6        | 0         |
| 6 ÷ 2    | 3        | 0         |
| 3 ÷ 2    | 1        | 1         |
| 1 ÷ 2    | 0        | 1         |

Bottom to top:

```text
11001
```

Therefore:

```text
25 = 11001₂
```

---

# Why Bottom to Top?

Every division gives:

```text
n % 2
```

which is the Least Significant Bit (LSB).

Matlab hume bits milti hain:

```text
Right → Left
```

Binary likhte hain:

```text
Left → Right
```

Isliye reverse karna padta hai.

---

# 3. Fractional Decimal to Binary

Example:

```text
0.375
```

Integer part me divide by 2 karte the.

Fraction part me:

```text
Multiply by 2
```

karte hain.

---

# Step 1

```text
0.375 × 2 = 0.75
```

Bit:

```text
0
```

---

# Step 2

```text
0.75 × 2 = 1.5
```

Bit:

```text
1
```

Keep:

```text
0.5
```

---

# Step 3

```text
0.5 × 2 = 1.0
```

Bit:

```text
1
```

Stop.

---

Answer:

```text
0.375 = 0.011₂
```

Verification:

```text
0×2⁻¹ +
1×2⁻² +
1×2⁻³
```

```text
0 + 0.25 + 0.125
```

```text
= 0.375
```

---

# Why Multiplication by 2?

Integer conversion me:

```text
Last bit extract karni thi
```

Fraction conversion me:

```text
Next bit extract karni hoti hai
```

Aur multiplication by 2 exactly wahi karta hai.

---

# 4. Mixed Decimal Numbers

Example:

```text
38.375
```

---

## Integer Part

Convert:

```text
38
```

Repeated division:

```text
38 → 19 R0
19 → 9  R1
9  → 4  R1
4  → 2  R0
2  → 1  R0
1  → 0  R1
```

Bottom to top:

```text
100110
```

---

## Fraction Part

Convert:

```text
0.375
```

Result:

```text
0.011
```

---

## Final Answer

Combine both:

```text
38.375
=
100110.011₂
```

---

# What About 38.54545?

Same process.

Integer Part:

```text
38
=
100110₂
```

Fraction Part:

```text
0.54545
```

Repeatedly multiply by 2.

```text
0.54545 × 2 = 1.0909 → 1
0.0909 × 2 = 0.1818 → 0
0.1818 × 2 = 0.3636 → 0
0.3636 × 2 = 0.7272 → 0
0.7272 × 2 = 1.4544 → 1
...
```

Result continues forever.

```text
100110.10001...
```

---

# Important Observation

Most decimal fractions cannot be represented exactly in binary.

Just like:

```text
1/3 = 0.333333...
```

never ends in decimal.

Similarly:

```text
0.1
```

never ends in binary.

Therefore computers store an approximation.

---
