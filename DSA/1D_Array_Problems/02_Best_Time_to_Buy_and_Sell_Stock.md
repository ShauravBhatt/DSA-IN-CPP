# Best Time to Buy and Sell Stock

## 1. Problem
Problem Link : https://leetcode.com/problems/best-time-to-buy-and-sell-stock/description/

Hume stock prices ka array diya hai:

```text
prices[i] = day i par stock ka price
```

Hume:
- ek din stock **buy** karna hai
- kisi **future day** par sell karna hai
- maximum possible profit return karna hai

Profit:

```text
profit = selling price - buying price
```

Agar profit possible nahi hai, answer `0`.

Example:

```text
prices = [7, 1, 5, 3, 6, 4]

Buy  at 1
Sell at 6

Profit = 6 - 1 = 5
```

Important condition:

```text
buy day < sell day
```

---

## 2. Brute Force

Har possible buying day aur uske baad har possible selling day ko try karo.

Har pair ke liye:

```text
profit = prices[j] - prices[i]
```

aur maximum profit store karo.

Complexity:

```text
Time  = O(n²)
Space = O(1)
```

But is problem ko `O(n)` mein solve kiya ja sakta hai.

---

## 3. Kya Sirf Minimum aur Maximum Nikaal Sakte Hain?

Natural thought:

> Sabse cheap price par buy aur sabse expensive price par sell karunga.

But sirf global minimum aur maximum enough nahi hain.

Example:

```text
[7, 1, 5, 3, 6, 4]
```

Minimum = `1`

Maximum = `7`

Agar simply:

```text
7 - 1 = 6
```

karo, toh wrong answer milega.

Kyun?

`7` pehle aaya tha aur `1` baad mein.

Stock mein pehle buy aur baad mein sell karna compulsory hai.

So:

```text
buy day < sell day
```

Order matters.

---

## 4. Better Way of Thinking

Instead of asking:

> Best buy day aur best sell day ek saath kaunsa hai?

Har day ko **selling day** maan lo.

Suppose aaj price:

```text
prices[i]
```

hai.

Agar aaj sell karna hai, toh maximum profit tab milega jab humne aaj se pehle ka **sabse cheap price** par buy kiya ho.

Therefore:

```text
Today's Profit
= Today's Price - Minimum Price Seen Before Today
```

Ye main observation hai.

---

## 5. Example

```text
prices = [7, 1, 5, 3, 6, 4]
```

### Day 0 — price 7

Abhi koi previous day nahi hai.

So:

```text
bestBuy = 7
maxProfit = 0
```

### Day 1 — price 1

Future ke liye `1` better buying price hai:

```text
bestBuy = min(7, 1)
        = 1
```

Abhi sell karne ke liye previous day ka valid buying price `7` hai, jisse profit nahi banega. We simply keep `maxProfit = 0`.

### Day 2 — price 5

Aaj sell karne par:

```text
5 - 1 = 4
```

So:

```text
maxProfit = 4
```

### Day 3 — price 3

```text
3 - 1 = 2
```

Already `maxProfit = 4`, so no change.

### Day 4 — price 6

```text
6 - 1 = 5
```

So:

```text
maxProfit = 5
```

### Day 5 — price 4

```text
4 - 1 = 3
```

No improvement.

Final answer:

```text
5
```

---

## 6. Do Variables Enough Hain

### `bestBuy`

Ab tak dekhe gaye prices mein minimum price.

```text
bestBuy = minimum price seen so far
```

### `maxProfit`

Ab tak possible maximum profit.

```text
maxProfit = maximum profit seen so far
```

Har day:

1. Aaj sell karne par profit calculate karo.
2. `maxProfit` update karo.
3. Aaj ka price future ke liye new `bestBuy` ho sakta hai, so minimum update karo.

---

## 7. Dry Run

For:

```text
[7, 1, 5, 3, 6, 4]
```

| Day | Price | Best Buy So Far | Today's Profit | Max Profit |
|---:|---:|---:|---:|---:|
| 0 | 7 | 7 | — | 0 |
| 1 | 1 | 1 | — | 0 |
| 2 | 5 | 1 | 4 | 4 |
| 3 | 3 | 1 | 2 | 4 |
| 4 | 6 | 1 | 5 | 5 |
| 5 | 4 | 1 | 3 | 5 |

Answer:

```text
5
```

---

## 8. Important Loop Hole — Global Min/Max

Example:

```text
[7, 6, 4, 3, 1]
```

Global maximum:

```text
7
```

Global minimum:

```text
1
```

But:

```text
7 - 1 = 6
```

valid profit nahi hai because `1` comes after `7`.

Correct answer:

```text
0
```

So minimum price ko **past prices** se track karna hai, poore array se nahi.

---

## 9. Important Loop Hole — No Profit

Example:

```text
[7, 6, 4, 3, 1]
```

Har future price previous buying price se lower hai.

So every possible transaction gives a loss.

Problem negative profit return nahi karne ko kehti hai.

Therefore:

```text
maxProfit = 0
```

se start karna natural hai.

---

## 10. Important Loop Hole — Same Day Buy and Sell

Day `0` par hum sell nahi kar sakte because usse pehle koi buying day nahi hai.

Isliye:

```cpp
for (int i = 1; i < prices.size(); i++)
```

se loop start karna clean hai.

`prices[0]` ko initial `bestBuy` maan lo.

---

## 11. Why `bestBuy` Must Keep Updating

Example:

```text
[5, 4, 3, 2, 10]
```

Agar `bestBuy` ko sirf `5` rakha:

```text
10 - 5 = 5
```

But actual best transaction:

```text
Buy at 2
Sell at 10

Profit = 8
```

Therefore har day check karo:

```text
bestBuy = min(bestBuy, current price)
```

---

## 12. Final Logic

Start:

```text
bestBuy = prices[0]
maxProfit = 0
```

Then every future day:

```text
todayProfit = prices[i] - bestBuy
```

Maximum profit:

```text
maxProfit = max(maxProfit, todayProfit)
```

Future buying opportunities:

```text
bestBuy = min(bestBuy, prices[i])
```

Array ko sirf ek baar traverse karna enough hai.

---

## 13. Final Code

```cpp
class Solution {
public:
    int maxProfit(vector<int>& prices) {

        int bestBuy = prices[0];
        int maxProfit = 0;

        for (int i = 1; i < prices.size(); i++) {

            int todayProfit = prices[i] - bestBuy;

            maxProfit = max(maxProfit, todayProfit);

            bestBuy = min(bestBuy, prices[i]);
        }

        return maxProfit;
    }
};
```

---

## 14. Complexity

```text
Time Complexity  = O(n)
Space Complexity = O(1)
```

Array ko ek hi baar traverse kiya hai.

---

## 15. Useful Test Cases

### Normal case

```text
[7, 1, 5, 3, 6, 4]
→ 5
```

### Completely decreasing

```text
[7, 6, 4, 3, 1]
→ 0
```

Checks whether negative profit incorrectly return ho raha hai.

### Completely increasing

```text
[1, 2, 3, 4, 5]
→ 4
```

Checks whether minimum buying price correctly maintain ho raha hai.

### One element

```text
[5]
→ 0
```

There is no future day to sell.

### Minimum occurs late

```text
[5, 4, 3, 2, 10]
→ 8
```

Checks whether `bestBuy` properly update ho raha hai.

### Maximum occurs before minimum

```text
[10, 5, 1]
→ 0
```

Checks the most important rule: buy must happen before sell.

---

## 16. Core Idea

Har day ko selling day assume karo.

Aaj ke liye best possible buying price:

```text
minimum price seen before today
```

Then:

```text
profit = today's price - best previous buying price
```

Throughout the array:

```text
bestBuy   → minimum price so far
maxProfit → maximum profit so far
```

This gives an `O(n)` time and `O(1)` space solution.
