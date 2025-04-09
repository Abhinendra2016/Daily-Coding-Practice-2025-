# Problem 3375: Minimum Operations to Make Array Values Equal to K

Given an integer array `nums` and an integer `k`, your goal is to perform the **minimum number of operations** to make all elements in the array equal to `k`.

---

## 💡 Operation Rules

- Choose an integer `h` which is **valid**:
  - A number is **valid** if all `nums[i] > h` are **identical**.
- For all `nums[i] > h`, update `nums[i] = h`.

Return the **minimum number of such operations** needed to make all elements in the array equal to `k`.

If it's **not possible**, return `-1`.

---

## 🧪 Examples

### Example 1:

Input: nums = [5,2,5,4,5], k = 2 Output: 2

Explanation: 1st operation with h = 4 → [4, 2, 4, 4, 4] 2nd operation with h = 2 → [2, 2, 2, 2, 2]

### Example 2:

Input: nums = [2,1,2], k = 2 Output: -1

Explanation: We can't increase 1 to 2 using valid operations.

### Example 3:

Input: nums = [9,7,5,3], k = 1 Output: 4

Explanation: Perform operations with h = 7 → 5 → 3 → 1.


---

## 🔒 Constraints

- `1 <= nums.length <= 100`
- `1 <= nums[i] <= 100`
- `1 <= k <= 100`

---

## ✅ Solution

The main idea is:

- If the **minimum element** in the array is less than `k`, it's **impossible** to reach `k` → return `-1`.<br>
- If `k` is less than all values, the number of operations equals the **number of unique elements**.<br>
- If `k` is already in the array and is the **smallest**, subtract 1 from the unique element count since we don’t need an operation for `k`.
<br>
---

## 🧠 Code

```python
class Solution:
  def minOperations(self, nums: list[int], k: int) -> int:
    numsSet = set(nums)
    mn = min(nums)
    if mn < k:
      return -1
    if mn > k:
      return len(numsSet)
    return len(numsSet) - 1
```
<h2>Time Complexity</h2> O(n) — for creating a set and finding the minimum value.<br>
 <h2> Space Complexity</h2> O(n) — for storing unique elements in a set.<br>

