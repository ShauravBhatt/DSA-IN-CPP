# 1. Continuous Character Square Pattern

## Question

For `n = 3`

```text
ABC
DEF
GHI
```

## Hint

- Total rows = `n`
- Total columns = `n`
- Character continuously increase ho raha hai.

```text
A B C
D E F
G H I
```

## Solution

```cpp
int n = 3;
char ch = 'A';

for(int i = 1; i <= n; i++)
{
    for(int j = 1; j <= n; j++)
    {
        cout << ch;
        ch++;
    }
    cout << endl;
}
```

## Idea

- Ek character variable lo.
- Har print ke baad usse increment kar do.
- Character poore pattern me continuously chalta rahega.

---

# 2. Character Row Shift Pattern

## Question

For `n = 3`

```text
ABC
BCD
CDE
```

## Hint

Observe the starting character of each row.

```text
Row 1 → A
Row 2 → B
Row 3 → C
```

## Solution

```cpp
int n = 3;

for(int i = 1; i <= n; i++)
{
    char ch = 'A' + i - 1;

    for(int j = 1; j <= n; j++)
    {
        cout << ch;
        ch++;
    }

    cout << endl;
}
```

## Idea

- Har row ka starting character change ho raha hai.
- Starting character:

```cpp
'A' + i - 1
```

- Uske baad character continuously increment hota hai.

---

# 3. Character Triangle Pattern

## Question

```text
A
BC
DEF
GHIJ
```

## Hint

Characters continuously increase ho rahe hain.

```text
Row 1 → 1 char
Row 2 → 2 char
Row 3 → 3 char
Row 4 → 4 char
```

## Solution

```cpp
int n = 4;
char ch = 'A';

for(int i = 1; i <= n; i++)
{
    for(int j = 1; j <= i; j++)
    {
        cout << ch;
        ch++;
    }

    cout << endl;
}
```

## Idea

- Triangle pattern hai.
- Inner loop row number tak chalega.
- Character continuously increment hoga.

---

# 4. Character Increment Row Pattern

## Question

```text
A
BC
CDE
DEFG
```

## Hint

Observe starting character.

```text
Row 1 → A
Row 2 → B
Row 3 → C
Row 4 → D
```

Har row ka start character change ho raha hai.

## Solution

```cpp
int n = 4;

for(int i = 1; i <= n; i++)
{
    char ch = 'A' + i - 1;

    for(int j = 1; j <= i; j++)
    {
        cout << ch;
        ch++;
    }

    cout << endl;
}
```

## Idea

- Har row me naya starting character.
- Uske baad character increment.

---

# 5. Reverse Character Triangle

## Question

```text
D
CD
BCD
ABCD
```

## Hint

Observe row start.

```text
Row 1 → D
Row 2 → C
Row 3 → B
Row 4 → A
```

Character reverse side se start ho raha hai.

## Solution

```cpp
int n = 4;

for(int i = 1; i <= n; i++)
{
    char ch = 'A' + n - i;

    for(int j = 1; j <= i; j++)
    {
        cout << ch;
        ch++;
    }

    cout << endl;
}
```

## Idea

Starting character:

```cpp
'A' + n - i
```

Baaki character normal increment.

---

# 6. Right Aligned Star Triangle

## Question

```text
   *
  **
 ***
****
```

## Hint

Har row me:

```text
Spaces + Stars
```

Example:

```text
Row 1 → 3 spaces + 1 star
Row 2 → 2 spaces + 2 stars
Row 3 → 1 space  + 3 stars
Row 4 → 0 space  + 4 stars
```

## Solution

```cpp
int n = 4;

for(int i = 1; i <= n; i++)
{
    for(int j = 1; j <= n - i; j++)
    {
        cout << " ";
    }

    for(int j = 1; j <= i; j++)
    {
        cout << "*";
    }

    cout << endl;
}
```

## Idea

- Spaces decrease.
- Stars increase.

---

# 7. Inverted Star Triangle

## Question

```text
****
***
**
*
```

## Hint

Stars har row me 1 kam ho rahe hain.

## Solution

```cpp
int n = 4;

for(int i = n; i >= 1; i--)
{
    for(int j = 1; j <= i; j++)
    {
        cout << "*";
    }

    cout << endl;
}
```

## Idea

Outer loop reverse chala do.

---

# 8. Right Aligned Inverted Star Triangle

## Question

```text
****
 ***
  **
   *
```

## Hint

Har row:

```text
Spaces increase
Stars decrease
```

## Solution

```cpp
int n = 4;

for(int i = n; i >= 1; i--)
{
    for(int j = 1; j <= n - i; j++)
    {
        cout << " ";
    }

    for(int j = 1; j <= i; j++)
    {
        cout << "*";
    }

    cout << endl;
}
```

## Idea

Pattern = Spaces + Stars

---

# 9. Number Space Pattern

## Question

```text
1111
 222
  33
   4
```

## Hint

Observe:

```text
Spaces increase
Numbers decrease
```

## Solution

```cpp
int n = 4;

for(int i = 1; i <= n; i++)
{
    for(int j = 1; j < i; j++)
    {
        cout << " ";
    }

    for(int j = 1; j <= n - i + 1; j++)
    {
        cout << i;
    }

    cout << endl;
}
```

## Idea

- Left spaces increase.
- Number count decrease.

---

# 10. Reverse Number Triangle

## Question

```text
   1
  22
 333
4444
```

## Hint

Observe:

```text
Spaces decrease
Numbers increase
```

## Solution

```cpp
int n = 4;

for(int i = 1; i <= n; i++)
{
    for(int j = 1; j <= n - i; j++)
    {
        cout << " ";
    }

    for(int j = 1; j <= i; j++)
    {
        cout << i;
    }

    cout << endl;
}
```

## Idea

Opposite of previous pattern.

---

# 11. Floyd's Triangle

## Question

```text
      1
    2 3
  4 5 6
7 8 9 10
```

## Hint

Numbers continuously increase ho rahe hain.

```text
1
2 3
4 5 6
7 8 9 10
```

Isliye ek separate variable chahiye.

## Solution

```cpp
int n = 4;
int num = 1;

for(int i = 1; i <= n; i++)
{
    for(int j = 1; j <= n - i; j++)
    {
        cout << "  ";
    }

    for(int j = 1; j <= i; j++)
    {
        cout << num << " ";
        num++;
    }

    cout << endl;
}
```

## Idea

- `num` poore pattern me continuously increase hota hai.
- Row ya column se koi relation nahi.

---

# 12. Palindrome Number Pyramid

## Question

```text
   1
  121
 12321
1234321
```

## Hint

Pattern ko 3 parts me dekho.

```text
Spaces
Increasing Numbers
Decreasing Numbers
```

Example:

```text
12321

123
 21
```

## Solution

```cpp
int n = 4;

for(int i = 1; i <= n; i++)
{
    for(int j = 1; j <= n - i; j++)
    {
        cout << " ";
    }

    for(int j = 1; j <= i; j++)
    {
        cout << j;
    }

    for(int j = i - 1; j >= 1; j--)
    {
        cout << j;
    }

    cout << endl;
}
```

## Idea

Pattern =

```text
Spaces
Increasing numbers
Decreasing numbers
```

3 blocks ko combine karo.

---

# 13. Fancy Number-Star Pattern

## Question

```text
123454321
1234**4321
123****321
12******21
1********1
```

## Hint

Har row me pattern ko 3 blocks me divide karo.

### Row 1

```text
12345
54321
```

### Row 2

```text
1234
**
4321
```

### Row 3

```text
123
****
321
```

Observe:

- Left numbers decrease
- Stars increase by 2
- Right numbers mirror image

## Observation

For row `i`

```cpp
Left Numbers  = n - i + 1
Stars         = 2 * (i - 1)
Right Numbers = n - i + 1
```

## Solution

```cpp
int n = 5;

for(int i = 1; i <= n; i++)
{
    // Left Numbers
    for(int j = 1; j <= n - i + 1; j++)
    {
        cout << j;
    }

    // Stars
    for(int j = 1; j <= 2 * (i - 1); j++)
    {
        cout << "*";
    }

    // Right Numbers
    for(int j = n - i + 1; j >= 1; j--)
    {
        cout << j;
    }

    cout << endl;
}
```

## Idea

Pattern ko ek saath mat dekho.