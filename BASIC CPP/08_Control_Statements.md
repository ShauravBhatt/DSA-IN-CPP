# Conditional Statements in C++

## Introduction

Conditional statements ka use program mein decision making ke liye hota hai. Program different conditions ke basis par alag-alag actions perform karta hai.

For example:

- Agar chai stock mein hai → Order confirm karo.
- Agar stock mein nahi hai → Order reject karo.

---

## Types of Conditional Statements in C++

### 1. if Statement

Condition true hone par code execute hota hai.

```cpp
#include <iostream>
using namespace std;

int main() {
    int age = 18;

    if (age >= 18) {
        cout << "You can vote";
    }

    return 0;
}
```

---

### 2. if-else Statement

Condition true ho to ek block execute hota hai, otherwise doosra.

```cpp
#include <iostream>
using namespace std;

int main() {
    int age;

    cout << "Enter age: ";
    cin >> age;

    if (age >= 18) {
        cout << "Adult";
    } else {
        cout << "Minor";
    }

    return 0;
}
```

---

### 3. if-else if-else Statement

Multiple conditions check karne ke liye.

```cpp
#include <iostream>
using namespace std;

int main() {
    int marks;

    cout << "Enter marks: ";
    cin >> marks;

    if (marks >= 90) {
        cout << "Grade A";
    }
    else if (marks >= 75) {
        cout << "Grade B";
    }
    else if (marks >= 50) {
        cout << "Grade C";
    }
    else {
        cout << "Fail";
    }

    return 0;
}
```

---

### 4. Nested if Statement

Ek if ke andar doosra if.

```cpp
#include <iostream>
using namespace std;

int main() {
    int age = 20;
    bool hasLicense = true;

    if (age >= 18) {
        if (hasLicense) {
            cout << "Can drive";
        }
    }

    return 0;
}
```

---

### 5. Switch Statement

Multiple options mein se ek choose karne ke liye.

```cpp
#include <iostream>
using namespace std;

int main() {
    int choice;

    cout << "1. Tea\n";
    cout << "2. Coffee\n";
    cout << "3. Juice\n";
    cout << "Enter choice: ";

    cin >> choice;

    switch (choice) {
        case 1:
            cout << "Tea Selected";
            break;

        case 2:
            cout << "Coffee Selected";
            break;

        case 3:
            cout << "Juice Selected";
            break;

        default:
            cout << "Invalid Choice";
    }

    return 0;
}
```

---

# Taking Input in C++

Single integer input:

```cpp
int num;
cin >> num;
```

String input without spaces:

```cpp
string name;
cin >> name;
```

String input with spaces:

```cpp
string name;
getline(cin, name);
```

Character input:

```cpp
char ch;
cin >> ch;
```

Character input using cin.get():

```cpp
char ch;
ch = cin.get();
```

---

# Program: Check Positive, Negative or Zero

```cpp
#include <iostream>
using namespace std;

int main() {
    int num;

    cout << "Enter a number: ";
    cin >> num;

    if (num > 0) {
        cout << "Positive";
    }
    else if (num == 0) {
        cout << "Zero";
    }
    else {
        cout << "Negative";
    }

    return 0;
}
```

---

# Program: Find Greater Number

```cpp
#include <iostream>
using namespace std;

int main() {
    int num1, num2;

    cout << "Enter first number: ";
    cin >> num1;

    cout << "Enter second number: ";
    cin >> num2;

    if (num1 > num2) {
        cout << num1 << " is greater";
    }
    else if (num2 > num1) {
        cout << num2 << " is greater";
    }
    else {
        cout << "Both are equal";
    }

    return 0;
}
```

---

# Program: Character Category

```cpp
#include <iostream>
using namespace std;

int main() {
    char ch;

    cout << "Enter a character: ";
    cin >> ch;

    if (ch >= 'a' && ch <= 'z') {
        cout << "Lowercase Letter";
    }
    else if (ch >= 'A' && ch <= 'Z') {
        cout << "Uppercase Letter";
    }
    else if (ch >= '0' && ch <= '9') {
        cout << "Digit";
    }
    else {
        cout << "Special Character";
    }

    return 0;
}
```

---

# ASCII Value of Characters

Every character has a numeric ASCII value.

Examples:

| Character | ASCII |
|-----------|--------|
| A | 65 |
| a | 97 |
| 0 | 48 |
| 9 | 57 |

Program:

```cpp
#include <iostream>
using namespace std;

int main() {
    char ch;

    cout << "Enter character: ";
    cin >> ch;

    cout << "ASCII Value = " << (int)ch;

    return 0;
}
```

---

# Check Character Range

```cpp
#include <iostream>
using namespace std;

int main() {
    char ch;

    cout << "Enter character: ";
    cin >> ch;

    if (ch >= 'a' && ch <= 'z') {
        cout << "Lowercase Letter";
    }
    else if (ch >= 'A' && ch <= 'Z') {
        cout << "Uppercase Letter";
    }
    else if (ch >= '0' && ch <= '9') {
        cout << "Digit";
    }
    else {
        cout << "Special Character";
    }

    return 0;
}
```