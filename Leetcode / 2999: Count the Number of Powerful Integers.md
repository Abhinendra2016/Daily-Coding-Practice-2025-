# Problem 2999: Count the Number of Powerful Integers

You are given:
- An integer `start`
- An integer `finish`
- An integer `limit`
- A 0-indexed string `s` representing a positive integer

---

## 💡 Definition

A **powerful integer** is a positive integer `x` such that:
- `x` ends with the string `s` (i.e., `s` is a **suffix** of `x`)
- Every digit of `x` is less than or equal to `limit`

Return the **total number of powerful integers** within the range `[start..finish]`.

---

## 🧪 Examples

### Example 1:

Input: start = 1, finish = 6000, limit = 4, s = "124" Output: 5

Powerful integers = [124, 1124, 2124, 3124, 4124]

### Example 2:
Input: start = 15, finish = 215, limit = 6, s = "10" Output: 2
Powerful integers = [110, 210]
### Example 3:
Input: start = 1000, finish = 2000, limit = 4, s = "3000" Output: 0

No valid powerful integers in this range.

---

## 🔒 Constraints

- `1 <= start <= finish <= 10^15`
- `1 <= limit <= 9`
- `1 <= s.length <= floor(log10(finish)) + 1`
- `s` only consists of digits `<= limit`
- `s` does not have leading zeros

---

## ✅ Solution Overview

The approach uses **digit dynamic programming (digit DP)**:

- Count how many numbers up to `finish` end with `s` and are bounded by the `limit`.
- Subtract how many such numbers are up to `start - 1`.

---

## 🧠 Python Code

```python
from functools import cache

class Solution:
    def numberOfPowerfulInt(self, start: int, finish: int, limit: int, s: str) -> int:
        @cache
        def dfs(pos: int, lim: bool) -> int:
            if len(t) < n:
                return 0
            if len(t) - pos == n:
                return int(s <= t[pos:]) if lim else 1
            up = min(int(t[pos]) if lim else 9, limit)
            ans = 0
            for i in range(up + 1):
                ans += dfs(pos + 1, lim and i == int(t[pos]))
            return ans

        n = len(s)
        t = str(start - 1)
        a = dfs(0, True)
        dfs.cache_clear()
        t = str(finish)
        b = dfs(0, True)
        return b - a
```
<h2>Time Complexity</h2>

O(D * limit), where D = number of digits in finish
Memoization helps avoid redundant computations
<h2>Space Complexity</h2>

O(D * 2) for recursion depth and caching


