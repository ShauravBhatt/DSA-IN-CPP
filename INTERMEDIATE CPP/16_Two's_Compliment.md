# Two's Complement Notes

# 1. Why Do We Need Two's Complement?

Hum humans numbers ko aise likhte hain:

```text
+8
-8
+15
-15
```

Kyuki humare paas:

```text
+
-
```

jaise symbols hote hain.

---

Lekin computer ke paas sirf:

```text
0
1
```

hote hain.

Computer ko nahi pata:

```text
+
-
positive
negative
```

Usko sab kuch 0 aur 1 ke form me hi store karna padta hai.

Isliye question aaya:

> Computer negative numbers ko represent kaise kare?

---

# 2. First Attempt: Sign Bit Representation

Engineers ne socha:

```text
0 -> Positive
1 -> Negative
```

Example:

```text
+8 = 00001000

-8 = 10001000
```

Yahan first bit sign batati hai.

---

## Problem

Zero ke do forms ban gaye.

```text
+0 = 00000000

-0 = 10000000
```

Mathematically:

```text
0 = -0
```

Lekin storage alag.

Ye inefficient tha.

---

# 3. Second Attempt: One's Complement

Idea:

Negative number banane ke liye saare bits invert kar do.

Example:

```text
+8 = 00001000
```

Invert:

```text
11110111
```

So:

```text
-8 = 11110111
```

---

## Problem

Fir se do zero ban gaye.

```text
00000000 = +0

11111111 = -0
```

Problem solve nahi hui.

---

# 4. Final Solution: Two's Complement

Rule:

```text
Negative Number
=
Invert All Bits
+
1
```

---

# Example: Convert -8

Positive number:

```text
+8

00001000
```

---

## Step 1: Invert

```text
00001000

↓

11110111
```

---

## Step 2: Add 1

```text
11110111
00000001
--------
11111000
```

Final Answer:

```text
-8 = 11111000
```

---

# Why Add 1?

Sirf invert karne se One's Complement milta hai.

```text
00001000

↓

11110111
```

Lekin isse arithmetic properly work nahi karti.

Isliye:

```text
+1
```

add kiya jata hai.

Ye extra +1 hi One's Complement ko Two's Complement me convert karta hai.

---

# Most Important Idea

CPU kabhi nahi sochta:

```text
Ye -8 hai
```

Ya:

```text
Ye 248 hai
```

CPU sirf dekhta hai:

```text
11111000
```

Bas.

Ye sirf ek bit pattern hai.

---

# Interpretation Changes

Same bits:

```text
11111000
```

---

If unsigned:

```text
11111000 = 248
```

---

If signed:

```text
11111000 = -8
```

---

Important:

```text
Bits same
Meaning different
```

---

# Why Two's Complement Became Popular?

Engineers chahte the ki:

```text
Addition Circuit
```

hi use ho.

Alag subtraction circuit na banana pade.

---

Check:

```text
+8 = 00001000

-8 = 11111000
```

Add:

```text
00001000
11111000
---------
100000000
```

Extra carry:

```text
1
```

drop ho jayegi.

Remaining:

```text
00000000
```

Result:

```text
8 + (-8) = 0
```

Perfect.

---

# Binary Addition Refresher

Rules:

```text
0 + 0 = 0

0 + 1 = 1

1 + 0 = 1

1 + 1 = 10
```

Important:

```text
1 + 1
```

gives:

```text
Result = 0
Carry  = 1
```

Exactly like:

```text
9 + 1 = 10
```

in decimal.

---

# Verification of -8

Take:

```text
11111000
```

Add:

```text
00001000
```

```text
11111000
00001000
---------
100000000
```

Carry removed:

```text
00000000
```

Therefore:

```text
11111000
```

behaves exactly like:

```text
-8
```

because:

```text
(-8) + 8 = 0
```

---

# Signed vs Unsigned

## Unsigned Integer

All bits store positive values.

8-bit range:

```text
0 to 255
```

---

## Signed Integer

Half range positive.

Half range negative.

8-bit range:

```text
-128 to +127
```

---

Example:

```text
11111000
```

Unsigned:

```text
248
```

Signed:

```text
-8
```

---

# Interview One-Liner

> Two's Complement is a method of representing negative numbers in binary such that the same addition hardware can be used for both positive and negative arithmetic.
