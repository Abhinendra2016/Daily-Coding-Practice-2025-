# Problem 416: Partition Equal Subset Sum

Given an integer array `nums`, return `true` if you can partition the array into **two subsets** such that the **sum of elements** in both subsets is equal. Otherwise, return `false`.

---

## Examples

### Example 1:

Input: nums = [1, 5, 11, 5] Output: true Explanation: The array can be partitioned as [1, 5, 5] and [11], both summing to 11.

### Example 2:

Input: nums = [1, 2, 3, 5] Output: false Explanation: No partition exists that divides the array into equal sum subsets.

---

## Constraints

- `1 <= nums.length <= 200`
- `1 <= nums[i] <= 100`

---

## Solution

We use a **Dynamic Programming (0/1 Knapsack)** approach. If the total sum is odd, partitioning equally is impossible. Otherwise, we try to find a subset of elements that sum up to `total_sum // 2`.

```python
class Solution:
  def canPartition(self, nums: list[int]) -> bool:
    summ = sum(nums)
    if summ % 2 == 1:
      return False
    return self.knapsack_(nums, summ // 2)
  def knapsack_(self, nums: list[int], subsetSum: int) -> bool:
    n = len(nums)
    dp = [[False] * (subsetSum + 1) for _ in range(n + 1)]
    dp[0][0] = True

    for i in range(1, n + 1):
      num = nums[i - 1]
      for j in range(subsetSum + 1):
        if j < num:
          dp[i][j] = dp[i - 1][j]
        else:
          dp[i][j] = dp[i - 1][j] or dp[i - 1][j - num]

    return dp[n][subsetSum]
```
<h2> Time Complexity</h2><br>
O(n * subsetSum) = O(n * (sum(nums) / 2)) Where `n` is the number of elements in `nums`. <br>
<h2>💾Space Complexity</h2><br>
O(n * subsetSum) for the DP table. This can be optimized to O(subsetSum) using a 1D array.
