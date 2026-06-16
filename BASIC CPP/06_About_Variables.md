# Variables, Declaration, Initialization & Assignment
### Beginner-Friendly Guide

Programming start karte time ye 4 terms bahut frequently use hoti hain:

1. Variable
2. Declaration
3. Initialization
4. Assignment

In sabka relation hai, but ye same cheez nahi hain.

---

# 1. Variable

Variable ek **named memory location** hota hai jahan hum data store karte hain.

Simple words mein:

> Variable = Ek labeled box jisme value store kar sakte hain.

### Example

```c
int age;
```

Yahan `age` ek variable hai.

---

## Real-Life Analogy

Maan lo tumhare paas ek box hai:

```text
+-------+
| age   |
+-------+
```

Ye box hi variable hai.

Abhi box bana hai, lekin andar kuch rakha nahi gaya.

---

# 2. Declaration

Declaration ka matlab hai compiler ko batana:

> "Mujhe ek variable chahiye aur uska type ye hai."

### Syntax

```c
data_type variable_name;
```

### Example

```c
int age;
```

Explanation:

- `int` → Data Type
- `age` → Variable Name

Compiler ko pata chal gaya:

> "Ek integer variable `age` exist karta hai."

---

## Important Point

Declaration sirf variable introduce karta hai.

Value dena zaroori nahi hai.

```c
int age;
```

Yahan:

✅ Variable declared hai

❌ Value assign nahi hui

---

# 3. Initialization

Initialization ka matlab:

> Variable create karte hi usko first value dena.

### Syntax

```c
data_type variable_name = value;
```

### Example

```c
int age = 20;
```

Yahan do kaam ho rahe hain:

```c
int age
```

→ Declaration

Aur

```c
= 20
```

→ Initialization

---

## Visual

```text
Create box:

+------+
| age  |
+------+

Put first value:

+------+
|  20  |
+------+
```

---

## Important Point

Initialization variable ke life ka **first assignment** hota hai.

Ye usually declaration ke saath hi hota hai.

```c
int age = 20;
```

---

# 4. Assignment

Assignment ka matlab:

> Variable ko value dena ya uski value change karna.

### Example

```c
int age;

age = 20;
```

Yahan:

```c
int age;
```

→ Declaration

Aur

```c
age = 20;
```

→ Assignment

---

## Value Change Karna

```c
age = 25;
```

Ab value update ho gayi.

Pehle:

```text
age = 20
```

Baad mein:

```text
age = 25
```

---

## Important Point

Assignment multiple times ho sakta hai.

```c
age = 20;
age = 25;
age = 30;
age = 35;
```

Har baar value update hogi.

---

# Side-by-Side Comparison

## Only Declaration

```c
int age;
```

Result:

✅ Variable created

❌ No value given

---

## Declaration + Initialization

```c
int age = 20;
```

Result:

✅ Variable created

✅ First value assigned

---

## Declaration Then Assignment

```c
int age;

age = 20;
```

Result:

✅ Variable declared

✅ Value assigned later

---


# Complete Example

```c
#include <stdio.h>

int main()
{
    int age;          // Declaration

    age = 20;         // Assignment

    int marks = 90;   // Declaration + Initialization

    marks = 95;       // Assignment

    printf("%d\n", age);
    printf("%d\n", marks);

    return 0;
}
```

### Output

```text
20
95
```

---

# Interview-Friendly Difference

| Term | Meaning |
|--------|---------|
| Variable | Memory location with a name |
| Declaration | Variable ko introduce karna |
| Initialization | Variable create karte hi first value dena |
| Assignment | Variable ko value dena ya update karna |

