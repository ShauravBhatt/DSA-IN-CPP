# Two-Dimensional Arrays (2D Arrays) in C++

# What is a Two-Dimensional Array?

A **Two-Dimensional Array (2D Array)** is simply an **array of arrays**.

Instead of storing values in a single line like a normal array, it stores values in the form of **rows and columns**, just like a matrix or table.

Think of it like an Excel sheet.

```text
      Columns

      0   1   2
    +---+---+---+
0   |10 |20 |30 |
    +---+---+---+
1   |40 |50 |60 |
    +---+---+---+
2   |70 |80 |90 |
    +---+---+---+

Rows
```

---

# 1D Array vs 2D Array

### 1D Array

Stores values in a single line.

```cpp
int arr[5] = {10,20,30,40,50};
```

Visualization:

```text
+----+----+----+----+----+
|10  |20  |30  |40  |50  |
+----+----+----+----+----+

 0    1    2    3    4
```

---

### 2D Array

Stores values in rows and columns.

```cpp
int matrix[3][3];
```

Visualization:

```text
+----+----+----+
|10  |20  |30  |
+----+----+----+
|40  |50  |60  |
+----+----+----+
|70  |80  |90  |
+----+----+----+
```

---

# Syntax

General Syntax:

```cpp
datatype arrayName[rows][columns];
```

Example:

```cpp
int matrix[3][3];
```

Meaning:

```text
Rows    = 3

Columns = 3
```

Total Elements:

```text
3 × 3 = 9
```

---

# Memory Representation

Although a 2D array looks like a table, memory mein ye **still contiguous (continuous)** hoti hai.

Suppose:

```cpp
int matrix[2][3] =
{
    {1,2,3},
    {4,5,6}
};
```

Theoretical View:

```text
+---+---+---+
|1  |2  |3  |
+---+---+---+
|4  |5  |6  |
+---+---+---+
```

---

Actual Memory:

```text
Address      Value

1000         1
1004         2
1008         3
1012         4
1016         5
1020         6
```

Notice:

```text
Rows alag dikh rahi hain,

but memory ek continuous block hai.
```

Ye concept baad mein Matrix Traversal aur Pointer Arithmetic mein bahut important hoga.

---

# Accessing Elements

Syntax:

```cpp
matrix[row][column]
```

Example:

```cpp
matrix[1][2]
```

Means:

```text
Row = 1

Column = 2
```

Output:

```text
6
```

---

# Taking Input in a 3×3 Matrix

Example:

```cpp
#include <iostream>
using namespace std;

int main()
{
    int matrix[3][3];

    cout << "Enter 9 elements:\n";

    for(int i=0; i<3; i++)
    {
        for(int j=0; j<3; j++)
        {
            cin >> matrix[i][j];
        }
    }

    cout << "\nMatrix:\n";

    for(int i=0; i<3; i++)
    {
        for(int j=0; j<3; j++)
        {
            cout << matrix[i][j] << " ";
        }

        cout << endl;
    }
}
```

Input:

```text
1 2 3
4 5 6
7 8 9
```

Output:

```text
1 2 3

4 5 6

7 8 9
```

---

# Different Ways to Initialize 2D Arrays

## Method 1 : Row-wise Initialization (Most Common)

```cpp
int matrix[2][3] =
{
    {1,2,3},
    {4,5,6}
};
```

Visualization:

```text
1 2 3

4 5 6
```

---

## Method 2 : Without Inner Curly Braces

C++ automatically fills row by row.

```cpp
int matrix[2][3] =
{
    1,2,3,
    4,5,6
};
```

Compiler understands:

```text
First 3 values

↓

First Row
,
Next 3 values

↓

Second Row
```

Result:

```text
1 2 3

4 5 6
```

---

## Method 3 : Omit Row Size

Compiler can calculate rows automatically.

```cpp
int matrix[][3] =
{
    {1,2,3},
    {4,5,6}
};
```

Rows:

```text
Automatically = 2
```

Columns **must** be provided.

Valid:

```cpp
int matrix[][3]
```

Invalid:

```cpp
int matrix[][]
```

Because compiler needs to know how many columns each row contains.

---

## Method 4 : Partial Initialization

```cpp
int matrix[2][3] =
{
    {1},
    {4}
};
```

Result:

```text
1 0 0

4 0 0
```

Remaining values become:

```text
0
```

---

# Why Do We Use 2D Arrays?

Whenever data naturally exists in rows and columns.

Examples:

```text
✓ Matrix Problems

✓ Chess Board

✓ Sudoku

✓ Game Boards

✓ Excel Sheets

✓ Seating Arrangement

✓ Image Pixels
```

---

# Traversing a 2D Array

To visit every element, we use **Nested Loops**.

Outer Loop:

```text
Rows
```

Inner Loop:

```text
Columns
```

Example:

```cpp
for(int i=0; i<3; i++)
{
    for(int j=0; j<3; j++)
    {
        cout << matrix[i][j] << " ";
    }

    cout << endl;
}
```

---

# Problem: Matrix Addition

Given two matrices of same size.

Add corresponding elements.

Example:

Matrix A

```text
1 2 3

4 5 6

7 8 9
```

Matrix B

```text
9 8 7

6 5 4

3 2 1
```

Result:

```text
10 10 10

10 10 10

10 10 10
```

---

# Logic

For every position:

```text
Result[i][j]

=

Matrix1[i][j]

+

Matrix2[i][j]
```

---

# Code

```cpp
#include <iostream>
using namespace std;

int main()
{
    int A[3][3];
    int B[3][3];
    int C[3][3];

    cout << "Enter Matrix A:\n";

    for(int i=0; i<3; i++)
    {
        for(int j=0; j<3; j++)
        {
            cin >> A[i][j];
        }
    }

    cout << "Enter Matrix B:\n";

    for(int i=0; i<3; i++)
    {
        for(int j=0; j<3; j++)
        {
            cin >> B[i][j];
        }
    }

    // Matrix Addition

    for(int i=0; i<3; i++)
    {
        for(int j=0; j<3; j++)
        {
            C[i][j] = A[i][j] + B[i][j];
        }
    }

    cout << "\nResult Matrix:\n";

    for(int i=0; i<3; i++)
    {
        for(int j=0; j<3; j++)
        {
            cout << C[i][j] << " ";
        }

        cout << endl;
    }
}
```

---

# Example

Input:

Matrix A

```text
1 2 3

4 5 6

7 8 9
```

Matrix B

```text
9 8 7

6 5 4

3 2 1
```

Output:

```text
10 10 10

10 10 10

10 10 10
```

The program simply adds elements present at the same row and column index.

Example:

```text
A[0][0] + B[0][0]

1 + 9

=

10
```

Similarly,

```text
A[1][2] + B[1][2]

6 + 4

=

10
```

and so on for every element of the matrix.