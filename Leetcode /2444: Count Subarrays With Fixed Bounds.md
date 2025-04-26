# Problem 2444: Count Subarrays With Fixed Bounds

You are given an **integer array** `nums` and two **integers** `minK` and `maxK`.

A **fixed-bound subarray** of `nums` is a subarray that satisfies **both** of the following conditions:

1. The **minimum value** in the subarray is equal to `minK`.
2. The **maximum value** in the subarray is equal to `maxK`.

🔁 A subarray is a **contiguous** part of an array.

Your task is to **return the number of fixed-bound subarrays**.

---

## 💡 Examples

### Example 1
**Input:**  
`nums = [1,3,5,2,7,5]`, `minK = 1`, `maxK = 5`  
**Output:** `2`  

**Explanation:**  
The fixed-bound subarrays are:  
- `[1,3,5]` (min = 1, max = 5)  
- `[1,3,5,2]` (min = 1, max = 5)  

---

### Example 2
**Input:**  
`nums = [1,1,1,1]`, `minK = 1`, `maxK = 1`  
**Output:** `10`  

**Explanation:**  
Every subarray contains only `1`, so all subarrays are fixed-bound subarrays.  
There are **10** total subarrays.

---

## ✅ Constraints

- `2 <= nums.length <= 10^5`  
- `1 <= nums[i], minK, maxK <= 10^6`

---

## 🚀 Solution

We iterate through the array and track the most recent positions of:
- An out-of-bound element (not between `minK` and `maxK`)
- The last occurrence of `minK`
- The last occurrence of `maxK`

Then, for each element, we calculate how many valid subarrays end at that index.

---

## 🧠 Code

```python
class Solution:
  def countSubarrays(self, nums: list[int], minK: int, maxK: int) -> int:
    ans = 0
    j = -1
    prevMinKIndex = -1
    prevMaxKIndex = -1
    for i, num in enumerate(nums):
      if num < minK or num > maxK:
        j = i
      if num == minK:
        prevMinKIndex = i
      if num == maxK:
        prevMaxKIndex = i
      ans += max(0, min(prevMinKIndex, prevMaxKIndex) - j)
    return ans     
```
<h2>Time Complexity</h2>

O(n) — We traverse the array once, keeping track of indices and performing constant-time operations.
<h2>Space Complexity</h2>

O(1) — No extra space is used beyond a few pointers and counters.

