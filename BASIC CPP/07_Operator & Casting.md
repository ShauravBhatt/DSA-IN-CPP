# Operators in C

## What is an Operator?

Operator ek special symbol hota hai jo operands (values ya variables) par operation perform karta hai.

### Example

```c
int a = 10;
int b = 5;

int sum = a + b;
```

Yahan:

- `a` aur `b` → Operands
- `+` → Operator

Operator ka kaam hai dono values ko add karna.

---

# Types of Operators

## 1. Arithmetic Operators

Mathematical calculations ke liye use hote hain.

| Operator | Meaning |
|----------|---------|
| `+` | Addition |
| `-` | Subtraction |
| `*` | Multiplication |
| `/` | Division |
| `%` | Modulus (Remainder) |

### Example

```c
int a = 10;
int b = 3;

a + b; // 13
a - b; // 7
a * b; // 30
a / b; // 3
a % b; // 1
```

---

## 2. Relational (Comparison) Operators

Do values compare karte hain.

Result:

```text
True (1)
False (0)
```

| Operator | Meaning |
|----------|---------|
| `==` | Equal To |
| `!=` | Not Equal To |
| `>` | Greater Than |
| `<` | Less Than |
| `>=` | Greater Than or Equal To |
| `<=` | Less Than or Equal To |

### Example

```c
10 > 5
```

Result:

```text
1
```

---

## 3. Logical Operators

Multiple conditions combine karne ke liye.

| Operator | Meaning |
|----------|---------|
| `&&` | Logical AND |
| `||` | Logical OR |
| `!` | Logical NOT |

### Example

```c
age >= 18 && age <= 60
```

Meaning:

```text
Age 18 se bada bhi ho
AND
60 se chhota bhi ho
```

---

## 4. Assignment Operators

Variable ko value assign karne ke liye.

| Operator | Meaning |
|----------|---------|
| `=` | Assign |
| `+=` | Add and Assign |
| `-=` | Subtract and Assign |
| `*=` | Multiply and Assign |
| `/=` | Divide and Assign |
| `%=` | Modulus and Assign |

### Example

```c
int x = 10;

x += 5;
```

Equivalent:

```c
x = x + 5;
```

Result:

```text
15
```

---

## 5. Increment & Decrement Operators

Value ko 1 se increase ya decrease karte hain.

| Operator | Meaning |
|----------|---------|
| `++` | Increment |
| `--` | Decrement |

### Example

```c
x++;
```

Equivalent:

```c
x = x + 1;
```

---

## 6. Bitwise Operators

Bits level par operation perform karte hain.

| Operator | Meaning |
|----------|---------|
| `&` | AND |
| `|` | OR |
| `^` | XOR |
| `~` | NOT |
| `<<` | Left Shift |
| `>>` | Right Shift |

### Example

```c
5 & 3
```

Binary:

```text
5 = 101
3 = 011
---------
    001
```

Result:

```text
1
```

---

## 7. Conditional (Ternary) Operator

Short form of if-else.

### Syntax

```c
condition ? value1 : value2;
```

### Example

```c
int result = (age >= 18) ? 1 : 0;
```

Meaning:

```text
If condition true → 1
Else → 0
```

---

## 8. sizeof Operator

Variable ya data type ki memory size batata hai.

### Example

```c
sizeof(int)
```

Output:

```text
4
```

(Depends on system)

---

# Type Casting

## What is Type Casting?

Ek data type ko dusre data type mein convert karna Type Casting kehlata hai.

### Example

```c
int a = 10;

float b = (float)a;
```

Result:

```text
10 → 10.0
```

---

# Types of Type Casting

Type Casting ke 2 types hote hain.

---

## 1. Implicit Type Casting (Automatic Conversion)

Compiler automatically conversion karta hai.

### Example

```c
int a = 10;

float b = a;
```

Compiler internally:

```c
float b = 10.0;
```

Kar deta hai.

### Conversion

```text
int → float
char → int
int → double
```

Automatic hota hai.

---

## 2. Explicit Type Casting (Manual Conversion)

Programmer khud conversion force karta hai.

### Syntax

```c
(new_type) value
```

### Example

```c
float price = 99.99;

int amount = (int)price;
```

Output:

```text
99
```

Decimal part remove ho gaya.

---

## Explicit Casting Examples

### int → float

```c
int a = 10;

float b = (float)a;
```

Output:

```text
10.0
```

---

### float → int

```c
float x = 12.75;

int y = (int)x;
```

Output:

```text
12
```

---

### char → int

```c
char ch = 'A';

int ascii = (int)ch;
```

Output:

```text
65
```

---

### int → char

```c
int num = 65;

char ch = (char)num;
```

Output:

```text
A
```
