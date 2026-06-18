# Pattern Printing in C++ (Using Nested `while` Loops)

## Basic Concept

Most pattern problems are solved using **nested loops**:

- **Outer loop (`i`)** → controls the rows.
- **Inner loop (`j`)** → controls what gets printed in each row.

### General Structure

```cpp
int i = 1;
while(i <= n)
{
    int j = 1;
    while(j <= ...)
    {
        // print something
        j++;
    }

    cout << endl;
    i++;
}
```

### Pattern ko Identify Kaise Kare?

Khud se ye questions pucho:

1. Kitni rows hain?
2. Har row mein kya change ho raha hai?
3. Har column mein kya change ho raha hai?
4. Koi aisa counter ya number hai jo continuously increase ho raha ho?

Jab in questions ke answers mil jaate hain, tab pattern ko samajhna aur build karna kaafi aasaan ho jaata hai.

---

# 1. Square Star Pattern

## Question

Print the following pattern:

For `n = 4`

```text
****
****
****
****
```

## Solution

```cpp
int i = 1;
while (i <= n)
{
    int j = 1;
    while (j <= n)
    {
        cout << "*";
        j++;
    }
    cout << "\n";
    i++;
}
```

## Idea

- Total rows = `n`
- Total columns = `n`
- Print `*` in every position.

---

# 2. Row Number Square Pattern

## Question

Print the following pattern:

For `n = 4`

```text
1111
2222
3333
4444
```

## Solution

```cpp
int i = 1;
while (i <= n)
{
    int j = 1;
    while (j <= n)
    {
        cout << i;
        j++;
    }
    i++;
    cout << "\n";
}
```

## Idea

Print the current row number (`i`) throughout the row.

---

# 3. Column Number Square Pattern

## Question

Print the following pattern:

For `n = 4`

```text
1234
1234
1234
1234
```

## Solution

```cpp
int i = 1;
while (i <= n)
{
    int j = 1;
    while (j <= n)
    {
        cout << j;
        j++;
    }
    i++;
    cout << "\n";
}
```

## Idea

Print the current column number (`j`).

---

# 4. Reverse Column Number Square Pattern

## Question

Print the following pattern:

For `n = 4`

```text
4321
4321
4321
4321
```

## Solution

```cpp
int i = 1;
while (i <= n)
{
    int j = 4;
    while (j >= 1)
    {
        cout << j;
        j--;
    }
    i++;
    cout << "\n";
}
```

## Idea

Start printing from the largest number and move backwards.

---

# 5. Continuous Number Square Pattern

## Question

Print the following pattern:

For `n = 4`

```text
1234
5678
9101112
13141516
```

## Solution

```cpp
int count = 1;

int i = 1;
while (i <= n)
{
    int j = 1;
    while (j <= n)
    {
        cout << count;
        j++;
        count++;
    }
    i++;
    cout << "\n";
}
```

## Idea

A separate variable `count` keeps increasing after every print.

---

# Triangle Patterns

In triangle patterns:

- Row number decides how many elements will be printed.
- Usually, row `i` prints `i` elements.

---

# 6. Star Triangle

## Question

Print the following pattern:

For `n = 4`

```text
*
**
***
****
```

## Solution

```cpp
int i = 1;
while (i <= n)
{
    int j = 1;
    while (j <= i)
    {
        cout << "*";
        j++;
    }
    i++;
    cout << "\n";
}
```

## Idea

Row 1 → 1 star

Row 2 → 2 stars

Row 3 → 3 stars

and so on.

---

# 7. Row Number Triangle

## Question

Print the following pattern:

For `n = 4`

```text
1
22
333
4444
```

## Solution

```cpp
int i = 1;
while (i <= n)
{
    int j = 1;
    while (j <= i)
    {
        cout << i;
        j++;
    }
    i++;
    cout << "\n";
}
```

## Idea

Print the row number `i`, exactly `i` times.

---

# 8. Continuous Number Triangle

## Question

Print the following pattern:

For `n = 4`

```text
1
23
456
78910
```

## Solution

```cpp
int count = 1;

int i = 1;
while (i <= n)
{
    int j = 1;
    while (j <= i)
    {
        cout << count;
        j++;
        count++;
    }
    i++;
    cout << "\n";
}
```

## Idea

A global counter keeps increasing continuously.

---

# 9. Increasing Sequence Triangle

## Question

Print the following pattern:

For `n = 4`

```text
1
23
345
4567
```

## Solution

```cpp
int i = 1;
while (i <= n)
{
    int j = i;
    while (j <= ((i * 2) - 1))
    {
        cout << j;
        j++;
    }
    i++;
    cout << "\n";
}
```

## Explanation

```cpp
Row 1:
j = 1 → 1

Row 2:
j = 2 → 23

Row 3:
j = 3 → 345

Row 4:
j = 4 → 4567
```

The row starts from `i` and prints `i` numbers.

---

# 10. Reverse Number Triangle

## Question

Print the following pattern:

For `n = 4`

```text
1
21
321
4321
```

## Solution

```cpp
int i = 1;
while (i <= n)
{
    int j = i;
    while (j >= 1)
    {
        cout << j;
        j--;
    }
    i++;
    cout << "\n";
}
```

## Explanation

```cpp
Row 1 -> 1

Row 2 -> 21

Row 3 -> 321

Row 4 -> 4321
```

Start from the row number and move backwards to 1.

---

# 11. Alphabet Square Pattern

## Question

Print the following pattern:

For `n = 4`

```text
ABCD
ABCD
ABCD
ABCD
```

## Solution

```cpp
int i = 1;
while (i <= n)
{
    int j = 1;
    int charAscii = 65;

    while (j <= n)
    {
        cout << static_cast<char>(charAscii);
        j++;
        charAscii++;
    }

    i++;
    cout << "\n";
}
```

## Idea

ASCII values:

```text
A = 65
B = 66
C = 67
D = 68
```

Increment the ASCII value after every print.

---

# 12. Alphabet Row Pattern

## Question

Print the following pattern:

For `n = 4`

```text
AAAA
BBBB
CCCC
DDDD
```

## Solution

```cpp
int i = 1;
int charAscii = 65;

while (i <= n)
{
    int j = 1;

    while (j <= n)
    {
        cout << static_cast<char>(charAscii);
        j++;
    }

    charAscii++;
    i++;
    cout << "\n";
}
```

## Idea

- One character is printed throughout a row.
- After completing the row, move to the next alphabet.

```text
Row 1 → A
Row 2 → B
Row 3 → C
Row 4 → D
```