# Problem 3272: Find the Count of Good Integers

You are given two positive integers `n` and `k`.

An integer `x` is called **k-palindromic** if:
- `x` is a **palindrome**
- `x` is **divisible by k**

An integer is called **good** if its digits can be **rearranged** to form a **k-palindromic** integer.  
> Leading zeros are **not allowed** before or after rearrangement.

---

## 🧪 Examples

### Example 1:
Input: n = 3, k = 5
Output: 27
**Explanation:**
Some of the good integers are:
- 551 → can be rearranged to form 515 (a k-palindromic integer)
- 525 → already a k-palindromic integer

---
### Example 2:

Input: n = 1, k = 4
Output: 2

**Explanation:**  
The two good integers are:  
- 4  
- 8  

---

### Example 3:
Input: n = 5, k = 6
Output: 2468

---

## 🔒 Constraints

- `1 <= n <= 10`  
- `1 <= k <= 9`

---

## ✅ Solution Overview

We:
1. Generate all possible half-palindromes of length `(n + 1) // 2`
2. Build the full palindrome by mirroring
3. Check if it's divisible by `k`
4. Count the number of permutations of the digits that form this k-palindromic integer  
   (while ensuring no leading zeros in permutations)

We use `collections.Counter` to count digits and `math.factorial` for permutations.

---
## 🧠 Python Code

```python
import math
import collections

class Solution:
  def countGoodIntegers(self, n: int, k: int) -> int:
    halfLength = (n + 1) // 2
    minHalf = 10**(halfLength - 1)
    maxHalf = 10**halfLength
    ans = 0
    seen = set()
    for num in range(minHalf, maxHalf):
      palindrome = str(num) + str(num)[::-1][n % 2:]
      sortedDigits = ''.join(sorted(palindrome))
      if int(palindrome) % k != 0 or sortedDigits in seen:
        continue
      seen.add(sortedDigits)
      digitCount = collections.Counter(palindrome)
      firstDigitChoices = n - digitCount['0']
      permutations = firstDigitChoices * math.factorial(n - 1)

      for freq in digitCount.values():
        permutations //= math.factorial(freq)

      ans += permutations

    return ans
```
<h2>Time Complexity</h2

Worst-case: O(9 * 10^((n+1)//2))<br>
(We iterate over all palindromes of half-length, then do factorial math per valid case)<br>
<h2>Space Complexity</h2

O(N) due to digit counting and memoization set<br>
