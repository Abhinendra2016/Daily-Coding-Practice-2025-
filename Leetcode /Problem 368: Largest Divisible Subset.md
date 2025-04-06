# Problem 368: Largest Divisible Subset

Given a set of **distinct positive integers** `nums`, return the **largest subset** `answer` such that **every pair** `(answer[i], answer[j])` satisfies:

- `answer[i] % answer[j] == 0`, or  
- `answer[j] % answer[i] == 0`

If there are multiple solutions, return any of them.

## Examples

### Example 1:
Input: nums = [1, 2, 3] Output: [1, 2] Explanation: [1, 3] is also accepted since 3 % 1 == 0.

### Example 2:

Input: nums = [1, 2, 4, 8] Output: [1, 2, 4, 8]

## Constraints

- `1 <= nums.length <= 1000`
- `1 <= nums[i] <= 2 * 10⁹`
- All the integers in `nums` are **unique**

## Solution

```python
class Solution:
  def largestDivisibleSubset(self, nums: list[int]) -> list[int]:
    n = len(nums)
    ans = []
    count = [1] * n
    prevIndex = [-1] * n
    maxCount = 0
    index = -1
    nums.sort()  # Sort to ensure divisibility chain is valid
    for i, num in enumerate(nums):
      for j in reversed(range(i)):
        if num % nums[j] == 0 and count[i] < count[j] + 1:
          count[i] = count[j] + 1
          prevIndex[i] = j
      if count[i] > maxCount:
        maxCount = count[i]
        index = i
    while index != -1:
      ans.append(nums[index])
      index = prevIndex[index]
    return ans

```
<h2>Time Complexity</h2> O(n²) — We iterate through each pair of elements in `nums` to build the dynamic programming table.<br>
<h2>Space Complexity</h2> O(n) — Arrays `count`, `prevIndex`, and `ans` each take linear space relative to the input size. <br>
<h2>Explanation</h2>
Sort the array to ensure we can compare smaller numbers with bigger ones for divisibility.<br>
Use Dynamic Programming to build:<br>
count[i]: length of the longest divisible subset ending at index i.
prevIndex[i]: the previous index in the chain to reconstruct the subset.
Track the maximum count and index to reconstruct the subset by backtracking using prevIndex.<br>
Return the reconstructed subset.