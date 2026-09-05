# Container With Most Water

## Problem
Problem Link: https://leetcode.com/problems/container-with-most-water/description/

Hume kuch vertical lines di gayi hain. Har line ki position uska index hai aur uski height array ke value se milti hai.

Hume **do lines choose karke maximum water** contain karna hai.

Example:

```text
height = [1, 8, 6, 2, 5, 4, 8, 3, 7]
```

Agar hum index `1` aur index `8` choose karein:

```text
height[1] = 8
height[8] = 7
```

Inke beech distance:

```text
8 - 1 = 7
```

Water ki maximum height:

```text
min(8, 7) = 7
```

Therefore:

```text
area = 7 × 7 = 49
```

Yahan se formula milta hai:

```text
area = min(height[i], height[j]) × (j - i)
```

---

## Pehla thought: brute force

Agar problem mein kaha gaya hai ki **koi bhi do lines choose karo**, toh natural approach hai:

> Har possible pair try karte hain.

For example:

```text
(0,1)
(0,2)
(0,3)
...
(1,2)
(1,3)
...
```

Har pair ka area calculate karenge aur maximum save karenge.

```cpp
for (int i = 0; i < n; i++) {
    for (int j = i + 1; j < n; j++) {

        int length = min(height[i], height[j]);
        int width = j - i;

        int area = length * width;

        maxArea = max(maxArea, area);
    }
}
```

Ye solution logically bilkul correct hai.

Lekin complexity:

```text
O(n²)
```

Agar `n` bahut bada hua, toh roughly `n × n` pairs check honge.

For example, agar `n = 10^5` hai, toh `10^10` level ke comparisons ho sakte hain.

Ye practically bahut zyada hai, isliye TLE aa sakta hai.

Ab yahan se actual problem solving start hoti hai.

---

# Brute Force Ko Dekhkar Optimization Kaise Sochen?

Brute force ko bas "O(n²) hai, two pointers laga do" kehna useful nahi hai.

Pehle dekho ki brute force mein **repeat kya ho raha hai**.

Hum har pair ke liye calculate kar rahe hain:

```text
height = min(height[i], height[j])
width  = j - i
```

Ab formula ko carefully dekho:

```text
area = min(height[i], height[j]) × (j - i)
```

Width tab maximum hogi jab:

```text
i = 0
j = n - 1
```

Toh ek natural thought aata hai:

> Agar width important hai, toh kya hum dono ends se start kar sakte hain?

Haan.

Set:

```text
left = 0
right = n - 1
```

Ab ek pair mil gaya.

Lekin problem ab ye hai:

> **Har step mein left ya right mein se kisko move karein?**

Yahi optimized solution ka main question hai.

---

# Left aur Right ko Move Karne Ka Logic

Suppose current pair:

```text
height[left]  = 8
height[right] = 5
```

Current container ki height:

```text
min(8, 5) = 5
```

Toh current area:

```text
5 × (right - left)
```

Ab dono pointers ko ek saath toh move nahi kar sakte.

Ek pointer move karna padega.

Do choices hain:

```text
1. left++
2. right--
```

Ab blindly choose nahi karna.

Let's reason.

---

## Agar Taller Side Ko Move Karein

Current:

```text
left  = 8
right = 5
```

Suppose `left++` kar diya.

Right wali stick `5` abhi bhi wahi hai.

New pair kuch bhi ho:

```text
newLeft
right = 5
```

New height:

```text
min(newLeft, 5)
```

Ab `newLeft` chahe:

```text
2
7
8
10
100
```

ho, effective height `5` se zyada nahi ho sakti.

Aur ek aur cheez:

```text
width = right - left
```

Left move karne se width chhoti ho gayi.

Matlab:

```text
height → maximum 5 hi
width  → decrease
```

Toh current taller side ko move karke better area milna possible nahi hai.

Iska matlab hum `left` ko safely discard kar sakte hain.

---

# Ab Shorter Side Ko Move Karke Dekho

Same situation:

```text
left  = 8
right = 5
```

Ab `right--` karte hain.

Suppose next right stick ki height:

```text
7
```

hai.

Ab pair:

```text
8 and 7
```

Effective height:

```text
min(8, 7) = 7
```

Height:

```text
5 → 7
```

improve ho gayi.

Width kam hui, but height improve hone ka chance mila.

Aur humein exactly yahi chahiye.

Isliye:

```text
shorter side ko move karo
```

---

# Lekin Ye Sirf Intuition Nahi Hai

Is decision ko properly prove kar sakte hain.

Suppose:

```text
height[left] < height[right]
```

Current height `height[left]` hai.

Ab current `left` ko fix rakho aur kisi bhi future `right` ko choose karo.

New area:

```text
min(height[left], height[newRight]) × (newRight - left)
```

Height part:

```text
min(height[left], height[newRight])
```

kabhi bhi `height[left]` se greater nahi ho sakta.

Aur because `newRight < right`:

```text
newRight - left < right - left
```

So:

```text
height cannot increase
width definitely decreases
```

Therefore current `left` ke saath future mein better area possible nahi hai.

So current `left` ko discard karna safe hai.

Isi tarah agar:

```text
height[right] < height[left]
```

toh current `right` ko discard karna safe hai.

Yahi proof two-pointer solution ko valid banata hai.

---

# Ab Algorithm Naturally Ban Raha Hai

Ab humein pata hai:

```text
left = 0
right = n - 1
```

Har iteration:

### 1. Current area calculate karo

```text
length = min(height[left], height[right])
width = right - left

currentArea = length × width
```

### 2. Maximum update karo

```text
maxArea = max(maxArea, currentArea)
```

### 3. Shorter side ko move karo

```text
if height[left] < height[right]:
    left++
else:
    right--
```

### 4. Repeat

Jab:

```text
left >= right
```

ho jaye, koi valid container pair nahi bachta.

---

# Equal Heights Ka Kya?

Suppose:

```text
height[left] = 5
height[right] = 5
```

Current height `5` hai.

Ab left move karo:

```text
min(newLeft, 5) <= 5
```

Right move karo:

```text
min(5, newRight) <= 5
```

Dono cases mein current height se greater height guaranteed nahi hai.

Isliye equal case mein kisi bhi ek side ko move kar sakte hain.

Code mein:

```cpp
if (height[left] < height[right]) {
    left++;
}
else {
    right--;
}
```

Equality mein `right--` hoga.

Ye valid hai.

---

# Dry Run

Take:

```text
height = [1, 8, 6, 2, 5, 4, 8, 3, 7]
```

Start:

```text
left = 0
right = 8
```

Values:

```text
height[left] = 1
height[right] = 7
```

Area:

```text
length = min(1, 7) = 1
width = 8 - 0 = 8

area = 1 × 8 = 8
```

So:

```text
maxArea = 8
```

Shorter side is left:

```text
1 < 7
```

Therefore:

```text
left++
```

Now:

```text
left = 1
right = 8
```

Values:

```text
8 and 7
```

Area:

```text
length = 7
width = 8 - 1 = 7

area = 7 × 7
     = 49
```

Update:

```text
maxArea = 49
```

Now right is shorter:

```text
7 < 8
```

So:

```text
right--
```

Now:

```text
left = 1
right = 7
```

Values:

```text
8 and 3
```

Area:

```text
length = 3
width = 6

area = 18
```

`maxArea` remains `49`.

Right is shorter, so:

```text
right--
```

The same process continues until:

```text
left >= right
```

Final answer:

```text
49
```

---

# Why Sorting Is Not Required

Two pointers dekhkar ek common thought aa sakta hai:

> "Array sorted nahi hai, toh two pointers kaise?"

Two pointers ka ek hi pattern nahi hota.

Kabhi sorted array ki wajah se movement decide hoti hai.

Yahan movement sorted order ki wajah se nahi ho rahi.

Yahan movement ka reason hai:

```text
shorter stick = bottleneck
```

Aur hum prove kar sakte hain ki taller side ko move karke current bottleneck ko improve nahi kiya ja sakta.

Isliye array sorted hona necessary nahi hai.

---

# Kuch Important Loopholes

## 1. Sirf tallest sticks choose karna

Maximum height alone answer decide nahi karti.

Area mein width bhi important hai:

```text
area = height × width
```

---

## 2. Sirf widest pair choose karna

Starting pair widest hota hai, but uski height bahut chhoti ho sakti hai.

Isliye har pointer position par area calculate karna zaroori hai.

---

## 3. Taller pointer ko move karna

Example:

```text
8 and 5
```

8 ko move karoge toh 5 bottleneck rahega aur width bhi decrease hogi.

Isliye shorter pointer move hota hai.

---

## 4. Maximum update karna bhool jana

Har pair par:

```cpp
maxArea = max(maxArea, currentArea);
```

hona chahiye.

Pointer move karne se pehle current pair ka area consider karna zaroori hai.

---

## 5. Loop condition

Use:

```cpp
while (left < right)
```

Jab `left == right` ho gaya, do different sticks nahi hain, so container possible nahi hai.

---

# Final Code

```cpp
class Solution {
public:
    int maxArea(vector<int>& height) {

        int left = 0;
        int right = height.size() - 1;
        int maxArea = 0;

        while (left < right) {

            int length = min(height[left], height[right]);
            int width = right - left;

            int currentArea = length * width;

            maxArea = max(maxArea, currentArea);

            if (height[left] < height[right]) {
                left++;
            }
            else {
                right--;
            }
        }

        return maxArea;
    }
};
```

---

# Complexity

Brute force:

```text
O(n²)
```

Optimized:

```text
O(n)
```

Reason ye hai ki har iteration mein ek pointer move karta hai:

```text
left++
```

ya:

```text
right--
```

Dono pointers kabhi peeche nahi jaate.

So total movements linear hain.

Extra space:

```text
O(1)
```

because sirf a few variables use ho rahe hain.
