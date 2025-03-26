# Problem 2033: Minimum Operations to Make a Uni-Value Grid

## Problem Statement

You are given a **2D integer grid** of size `m x n` and an integer `x`. In **one operation**, you can:

- **Add** `x` to any element in the grid.
- **Subtract** `x` from any element in the grid.

A **uni-value grid** is a grid where **all elements are equal**.

### **Objective**
Return the **minimum number of operations** required to make the grid **uni-value**.  
If it is **not possible**, return `-1`.

---

## Example 1:


Input: grid = [[2,4], [6,8]], x = 2

Output: 4

### **Explanation:**
We can make every element equal to **4** by doing the following:  
- **Add `x` to 2** once → `2 + 2 = 4`
- **Subtract `x` from 6** once → `6 - 2 = 4`
- **Subtract `x` from 8** twice → `8 - 2 - 2 = 4`  

**Total operations = 4**

---

## Example 2:


Input: grid = [[1,5], [2,3]], x = 1

Output: 5


### **Explanation:**
We can make every element equal to **3**.

---

## Example 3:


Input: grid = [[1,2], [3,4]], x = 2

Output: -1


### **Explanation:**
It is **impossible** to make all elements equal.

---

## Constraints:

- `m == grid.length`
- `n == grid[i].length`
- `1 <= m, n <= 10^5`
- `1 <= m * n <= 10^5`
- `1 <= x, grid[i][j] <= 10^4`

---

## **Solution Approach**

### **Key Idea**
- If `(grid[i][j] - min_value) % x` is **not the same for all elements**, it is **impossible** to make the grid **uni-value**.
- Otherwise, the optimal target value is the **median** of the sorted list.

### **Steps**
1. **Flatten the grid** into a **1D list** and sort it.
2. **Check divisibility condition**: If any `(value - min_value) % x ≠ 0`, return `-1`.
3. **Find the median** of the sorted list.
4. Compute **total moves** required to make all elements **equal to the median**.

---

## **Code Implementation**

```python
class Solution:
    def minOperations(self, grid: list[list[int]], x: int) -> int:
        arr = sorted([a for row in grid for a in row])
        if any((a - arr[0]) % x for a in arr):
            return -1
        ans = 0
        for a in arr:
            ans += abs(a - arr[len(arr) // 2]) // x
        return ans
```
<h2>Time Complexity</h2>

O(m × n log (m × n)) → Sorting the list.<BR>
O(m × n) → Checking divisibility & computing total operations.<BR>
Overall Complexity: O(m × n log (m × n))<BR>

<h2>Space Complexity</h2>

O(m × n) → To store the flattened grid.<BR>