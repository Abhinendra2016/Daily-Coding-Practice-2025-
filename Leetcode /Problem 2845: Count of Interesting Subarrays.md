# Problem 2845: Count of Interesting Subarrays

You are given a **0-indexed integer array** `nums`, an **integer** `modulo`, and an **integer** `k`.

Your task is to **find the count of subarrays** that are **interesting**.

A subarray `nums[l..r]` is interesting if the following condition holds:

> Let `cnt` be the number of indices `i` in the range `[l, r]` such that `nums[i] % modulo == k`. Then, `cnt % modulo == k`.

Return an integer denoting the **count of interesting subarrays**.

📌 **Note**: A subarray is a contiguous non-empty sequence of elements within an array.

---

## 💡 Examples

### Example 1
**Input**:  
`nums = [3, 2, 4]`, `modulo = 2`, `k = 1`  
**Output**: `3`  

**Explanation**:  
Interesting subarrays are:
- `[3]` → `cnt = 1` → `1 % 2 == 1 ✅`
- `[3, 2]` → `cnt = 1` → `1 % 2 == 1 ✅`
- `[3, 2, 4]` → `cnt = 1` → `1 % 2 == 1 ✅`

---

### Example 2
**Input**:  
`nums = [3, 1, 9, 6]`, `modulo = 3`, `k = 0`  
**Output**: `2`  

**Explanation**:  
Interesting subarrays are:
- `[1]` → `cnt = 0` → `0 % 3 == 0 ✅`
- `[3, 1, 9, 6]` → `cnt = 3` → `3 % 3 == 0 ✅`

---

## ✅ Constraints

- `1 <= nums.length <= 10^5`  
- `1 <= nums[i] <= 10^9`  
- `1 <= modulo <= 10^9`  
- `0 <= k < modulo`  

---

## 🚀 Solution

We can use a prefix sum + hash map optimization to track the number of prefix counts that satisfy the condition efficiently.

## 🧠 Code

```python
import collections

class Solution:
  def countInterestingSubarrays(
      self,
      nums: list[int],
      modulo: int,
      k: int,
  ) -> int:
    ans = 0
    prefix = 0  
    prefixCount = collections.Counter({0: 1})
    for num in nums:
      if num % modulo == k:
        prefix = (prefix + 1) % modulo
      ans += prefixCount[(prefix - k + modulo) % modulo]
      prefixCount[prefix] += 1
    return ans
```


<h2>Time Complexity</h2>

O(n) — We traverse the array once.<br>
Using a hash map for prefix count lookup and update takes constant time per operation.<br>
<h2>Space Complexity</h2>

O(modulo) — In the worst case, the prefix sum modulo values can span the range [0, modulo-1].<br>