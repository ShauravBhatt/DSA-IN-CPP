# Loops & Number Manipulation

## 1. Sum of Numbers from 1 to N

### Question

Ek positive integer `n` input lo aur `1` se `n` tak ke sabhi numbers ka sum print karo.

### Hint

- Ek `sum` variable lo.
- `1` se `n` tak loop chalao.
- Har number ko `sum` me add karte jao.

### Code

```cpp
#include <iostream>
using namespace std;

int main()
{
    int n;
    cin >> n;

    int sum = 0;

    for (int i = 1; i <= n; i++)
    {
        sum += i;
    }

    cout << sum;

    return 0;
}
```

---

## 2. Fibonacci Series

### Question

First `n` Fibonacci terms print karo.

### Hint

- First two terms: `0` and `1`
- Next term = previous two terms ka sum.

### Code

```cpp
#include <iostream>
using namespace std;

int main()
{
    int n;
    cin >> n;

    int first = 0;
    int second = 1;

    if (n >= 1)
        cout << first;

    if (n >= 2)
        cout << " " << second;

    for (int i = 3; i <= n; i++)
    {
        int next = first + second;
        cout << " " << next;

        first = second;
        second = next;
    }

    return 0;
}
```

---

## 3. Sum and Product of Digits

### Question

Ek number input lo aur uske digits ka sum aur product print karo.

### Hint

- Last digit nikalo using `% 10`
- Digit remove karo using `/ 10`
- Sum aur product update karte jao.

### Code

```cpp
#include <iostream>
using namespace std;

int main()
{
    int num;
    cin >> num;

    int sum = 0;
    int product = 1;

    while (num != 0)
    {
        int digit = num % 10;

        sum += digit;
        product *= digit;

        num /= 10;
    }

    cout << "Sum = " << sum << endl;
    cout << "Product = " << product << endl;

    return 0;
}
```

---

## 4. Reverse a Number

### Question

Ek number ka reverse print karo.

### Hint

- Har digit ko reverse number ke end me add karo.
- Formula:

```cpp
reversed = reversed * 10 + digit;
```

### Code

```cpp
#include <iostream>
using namespace std;

int main()
{
    int num;
    cin >> num;

    int reversed = 0;

    while (num != 0)
    {
        int digit = num % 10;

        reversed = reversed * 10 + digit;

        num /= 10;
    }

    cout << reversed;

    return 0;
}
```

---

## 5. Palindrome Number

### Question

Check karo ki number palindrome hai ya nahi.

### Hint

- Number reverse karo.
- Original aur reverse compare karo.

### Code

```cpp
#include <iostream>
using namespace std;

int main()
{
    int num;
    cin >> num;

    int original = num;
    int reversed = 0;

    while (num != 0)
    {
        int digit = num % 10;

        reversed = reversed * 10 + digit;

        num /= 10;
    }

    if (original == reversed)
        cout << "Palindrome";
    else
        cout << "Not Palindrome";

    return 0;
}
```

---

## 6. Largest Prime Digit

### Question

Number ke andar present sabse bada prime digit find karo.

### Prime Digits

```text
2 3 5 7
```

### Hint

- Ek-ek digit nikalo.
- Check karo ki digit `2`, `3`, `5`, ya `7` hai.
- Maximum store karte jao.

### Code

```cpp
#include <iostream>
using namespace std;

int main()
{
    int num;
    cin >> num;

    int largestPrime = -1;

    while (num != 0)
    {
        int digit = num % 10;

        if (digit == 2 || digit == 3 ||
            digit == 5 || digit == 7)
        {
            if (digit > largestPrime)
            {
                largestPrime = digit;
            }
        }

        num /= 10;
    }

    if (largestPrime == -1)
        cout << "No Prime Digit Found";
    else
        cout << largestPrime;

    return 0;
}
```

---

## Common Pattern

Almost har digit-based problem isi pattern par chalegi:

```cpp
while (num != 0)
{
    int digit = num % 10;

    // Process digit

    num /= 10;
}
```
