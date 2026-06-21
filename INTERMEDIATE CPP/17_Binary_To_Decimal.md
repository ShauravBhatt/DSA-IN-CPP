# Binary to Decimal Conversion Notes

# 1. Core Intuition

Decimal Number System:

```text
Base = 10
Digits = 0 to 9
```

Place values:

```text
538

=
5 × 10² +
3 × 10¹ +
8 × 10⁰
```

---

Binary Number System:

```text
Base = 2
Digits = 0 and 1
```

Place values:

```text
10110

=
1 × 2⁴ +
0 × 2³ +
1 × 2² +
1 × 2¹ +
0 × 2⁰
```

---

# Binary → Decimal Rule

For every bit:

```text
Bit × 2^(Position)
```

Then add all values.

---

# Example 1

Convert:

```text
101
```

Positions:

```text
1   0   1
2²  2¹  2⁰
```

Calculation:

```text
1×4 + 0×2 + 1×1
```

```text
4 + 0 + 1
```

```text
= 5
```

Therefore:

```text
101₂ = 5₁₀
```

---

# Example 2

Convert:

```text
1101
```

Positions:

```text
1   1   0   1
2³  2²  2¹  2⁰
```

Calculation:

```text
1×8 +
1×4 +
0×2 +
1×1
```

```text
8 + 4 + 0 + 1
```

```text
= 13
```

Therefore:

```text
1101₂ = 13₁₀
```

---

# Example 3

Convert:

```text
101101
```

Calculation:

```text
1×2⁵ +
0×2⁴ +
1×2³ +
1×2² +
0×2¹ +
1×2⁰
```

```text
32 + 0 + 8 + 4 + 0 + 1
```

```text
= 45
```

Therefore:

```text
101101₂ = 45₁₀
```

---

# Shortcut Method

Instead of calculating powers repeatedly:

```text
101101
```

Write powers:

```text
32 16 8 4 2 1
```

Now multiply:

```text
1×32
0×16
1×8
1×4
0×2
1×1
```

Add:

```text
32 + 8 + 4 + 1
```

```text
= 45
```

---

# 2. Binary Fraction to Decimal

After decimal point:

```text
2⁻¹
2⁻²
2⁻³
2⁻⁴
...
```

Important:

```text
2⁻¹ = 1/2 = 0.5

2⁻² = 1/4 = 0.25

2⁻³ = 1/8 = 0.125

2⁻⁴ = 1/16 = 0.0625
```

---

# Example 1

Convert:

```text
0.101
```

Calculation:

```text
1×2⁻¹ +
0×2⁻² +
1×2⁻³
```

```text
0.5 + 0 + 0.125
```

```text
= 0.625
```

Therefore:

```text
0.101₂ = 0.625₁₀
```

---

# Example 2

Convert:

```text
0.011
```

Calculation:

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

Therefore:

```text
0.011₂ = 0.375₁₀
```

---

# 3. Mixed Binary Numbers

Example:

```text
100110.011
```

Split into:

```text
Integer Part  = 100110
Fraction Part = .011
```

---

## Integer Part

```text
100110

=
1×32 +
0×16 +
0×8 +
1×4 +
1×2 +
0×1
```

```text
32 + 4 + 2
```

```text
= 38
```

---

## Fraction Part

```text
0.011

=
0×0.5 +
1×0.25 +
1×0.125
```

```text
0.25 + 0.125
```

```text
= 0.375
```

---

## Final Answer

```text
38 + 0.375
```

```text
= 38.375
```

Therefore:

```text
100110.011₂ = 38.375₁₀
```

---

# Binary to Decimal Code

## Method 1 (Beginner Friendly)

Input:

```text
1101
```

Output:

```text
13
```

---

## Logic

For every digit:

```text
Digit × 2^(Position)
```

Add everything.

---

## Code

```cpp
#include <iostream>
#include <cmath>
using namespace std;

int main()
{
    int binary;

    cin >> binary;

    int ans = 0;
    int i = 0;

    while(binary > 0)
    {
        int digit = binary % 10;

        ans = ans + digit * pow(2, i);

        binary = binary / 10;

        i++;
    }

    cout << ans;
}
```

---

# Dry Run

Input:

```text
1101
```

---

Iteration 1

```text
digit = 1

1 × 2⁰ = 1

ans = 1
```

Remaining:

```text
110
```

---

Iteration 2

```text
digit = 0

0 × 2¹ = 0

ans = 1
```

Remaining:

```text
11
```

---

Iteration 3

```text
digit = 1

1 × 2² = 4

ans = 5
```

Remaining:

```text
1
```

---

Iteration 4

```text
digit = 1

1 × 2³ = 8

ans = 13
```

Remaining:

```text
0
```

Stop.

Output:

```text
13
```

---

# Formula Used

```cpp
digit = binary % 10;
```

Extract last binary digit.

---

```cpp
ans += digit * pow(2, i);
```

Convert current bit into decimal contribution.

---

```cpp
binary /= 10;
```

Remove processed digit.

---

```cpp
i++;
```

Move to next power of 2.
