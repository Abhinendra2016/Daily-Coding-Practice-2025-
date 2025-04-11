# Problem 2999: Count the Number of Symmetric Integers

You are given two positive integers `low` and `high`.

An integer `x` consisting of `2 * n` digits is **symmetric** if the **sum of the first n digits** equals the **sum of the last n digits**.  
**Note:** Numbers with an **odd number of digits** are never symmetric.

---

## 🧪 Examples

### Example 1:

Input: low = 1, high = 100
Output: 9
Explanation:
There are 9 symmetric integers between 1 and 100:
[11, 22, 33, 44, 55, 66, 77, 88, 99]


### Example 2:

Input: low = 1200, high = 1230
Output: 4
Explanation:
The symmetric integers are:
[1203, 1212, 1221, 1230]
Each has 4 digits, and the sum of the first 2 digits equals the sum of the last 2.


---

## 🔒 Constraints

- `1 <= low <= high <= 10^4`

---

## ✅ Solution Overview

We only consider integers with even digits (2 or 4-digit numbers).  
The solution checks:
- If a 2-digit number is symmetric by comparing both digits.
- If a 4-digit number is symmetric by comparing the sum of the first two and the last two digits.

---

## 🧠 Python Code

```python
class Solution:
  def countSymmetricIntegers(self, low: int, high: int) -> int:
    def isSymmetricInteger(num: int) -> bool:
      if num >= 10 and num <= 99:
        return num // 10 == num % 10
      if num >= 1000 and num <= 9999:
        left = num // 100
        right = num % 100
        return left // 10 + left % 10 == right // 10 + right % 10
      return False    
    return sum(isSymmetricInteger(num) for num in range(low, high + 1))
```
<h2>Time Complexity</h2>

O(N) where N = high - low + 1
Each number is checked individually for symmetry.
<h2>Space Complexity</h2>

O(1) — Constant space used for variables.
