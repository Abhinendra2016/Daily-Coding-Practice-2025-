# Problem 3396: Minimum Number of Operations to Make Elements in Array Distinct

You are given an integer array `nums`. You need to ensure that all elements in the array are **distinct**. To achieve this, you can perform the following operation **any number of times**:

👉 **Operation**: Remove the first **3 elements** from the array. If the array has fewer than 3 elements, remove all of them.

> An empty array is considered to have all distinct elements.

---

## Examples

### Example 1:

Input: nums = [1,2,3,4,2,3,3,5,7] Output: 2

Explanation:

After 1st operation: [4, 2, 3, 3, 5, 7]
After 2nd operation: [3, 5, 7] → All elements are distinct

### Example 2:

Input: nums = [4,5,6,4,4] Output: 2

Explanation:

After 1st operation: [4, 4]
After 2nd operation: [] → Empty array (distinct by definition)

### Example 3:

Input: nums = [6,7,8,9] Output: 0

Explanation:

All elements are already distinct


---

## Constraints

- `1 <= nums.length <= 100`
- `1 <= nums[i] <= 100`

---

## Solution

We iterate through the array from the end and keep track of seen elements using a set. The moment we find a duplicate, we calculate how many 3-element removals are required to remove all elements up to (and including) that duplicate.

```python
class Solution:
  def minimumOperations(self, nums: list[int]) -> int:
    seen = set()
    for i, num in reversed(list(enumerate(nums))):
      if num in seen:
        return (i + 1 + 2) // 3
      seen.add(num)
    return 0
```
<h2>Time Complexity</h2> O(n), where `n` is the length of the array `nums`.<br>
<h2> Space Complexity</h2> O(n) in the worst case for the `seen` set.<br>

