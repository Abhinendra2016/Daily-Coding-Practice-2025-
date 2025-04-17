#  2176. Count Equal and Divisible Pairs in an Array

Given a 0-indexed integer array `nums` of length `n` and an integer `k`, return the number of **pairs (i, j)** where `0 <= i < j < n`, such that:

- `nums[i] == nums[j]`, and
- `(i * j)` is divisible by `k`.

---

## 🧠 Example 1

**Input:**  
`nums = [3,1,2,2,2,1,3]`, `k = 2`  
**Output:**  
`4`

**Explanation:**  
The valid pairs are:
- `(0, 6)` → 3 == 3 and 0 * 6 = 0 (divisible by 2)
- `(2, 3)` → 2 == 2 and 2 * 3 = 6 (divisible by 2)
- `(2, 4)` → 2 == 2 and 2 * 4 = 8 (divisible by 2)
- `(3, 4)` → 2 == 2 and 3 * 4 = 12 (divisible by 2)

---

## 🧠 Example 2

**Input:**  
`nums = [1,2,3,4]`, `k = 1`  
**Output:**  
`0`

**Explanation:**  
There are no repeated values, hence no valid pairs.

---

## 🧾 Constraints

- `1 <= nums.length <= 100`
- `1 <= nums[i], k <= 100`

---

## ✅ Solution (Python)

```python
import collections
import math

class Solution:
  def countPairs(self, nums: list[int], k: int) -> int:
    ans = 0
    numToIndices = collections.defaultdict(list)
    
    # Group indices by the same number
    for i, num in enumerate(nums):
      numToIndices[num].append(i)

    for indices in numToIndices.values():
      gcds = collections.Counter()
      for i in indices:
        gcd_i = math.gcd(i, k)
        for gcd_j, count in gcds.items():
          if gcd_i * gcd_j % k == 0:
            ans += count
        gcds[gcd_i] += 1

    return ans
```