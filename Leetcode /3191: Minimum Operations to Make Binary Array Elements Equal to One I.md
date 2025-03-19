# Problem 3191: Minimum Operations to Make Binary Array Elements Equal to One I

You are given a binary array `nums`.

You can do the following operation on the array any number of times (possibly zero):

- Choose any **3 consecutive elements** from the array and flip all of them.
- Flipping an element means changing its value from `0` to `1`, and from `1` to `0`.

Return the minimum number of operations required to make all elements in `nums` equal to `1`. If it is impossible, return `-1`.

## Example 1
**Input:**  
nums = [0,1,1,1,0,0]  
**Output:**  
3  
**Explanation:**  
We can do the following operations:
- Choose indices 0, 1 and 2 → nums = [1,0,0,1,0,0]
- Choose indices 1, 2 and 3 → nums = [1,1,1,0,0,0]
- Choose indices 3, 4 and 5 → nums = [1,1,1,1,1,1]

## Example 2
**Input:**  
nums = [0,1,1,1]  
**Output:**  
-1  
**Explanation:**  
It is impossible to make all elements equal to 1.

## Constraints

- 3 <= `nums.length` <= 10^5  
- 0 <= `nums[i]` <= 1

## Solution

```python
class Solution:
  def minOperations(self, nums: list[int]) -> int:
    ans = 0
    for i in range(len(nums) - 2):
      if nums[i] == 0:
        nums[i + 1] ^= 1
        nums[i + 2] ^= 1
        ans += 1
    return -1 if nums[-1] == 0 or nums[-2] == 0 else ans
```
<h2>Time Complexity</h2><br>
 The time complexity is **O(n)**, where `n` is the length of `nums`. We iterate through the array once. 
<h2>Space Complexity</h2> The space complexity is **O(1)** since we are modifying the input array in-place and using only a constant amount of additional space.<br>
 <h2>Explanation</h2> 
 1. We traverse the array from left to right. <br>
 2. Whenever we encounter a `0` at index `i`, we flip `nums[i+1]` and `nums[i+2]`. - This operation automatically changes `nums[i]` to `1` by flipping the 3 consecutive elements starting at `i`. <br>
 3. After completing the loop, we check the last two elements. If any of them is `0`, it's impossible to make the array all `1`s, so we return `-1`. <br>
 4. Otherwise, we return the count of the operations performed.<br>