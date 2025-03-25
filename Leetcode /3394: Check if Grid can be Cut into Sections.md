# Problem 3394: Check if Grid can be Cut into Sections
You are given an integer `n` representing the dimensions of an `n x n` grid, with the origin at the **bottom-left** corner of the grid. You are also given a **2D array** of coordinates `rectangles`, where `rectangles[i]` is in the form `[startx, starty, endx, endy]`, representing a **rectangle on the grid**. Each rectangle is defined as follows:

- `(startx, starty)`: The **bottom-left** corner of the rectangle.
- `(endx, endy)`: The **top-right** corner of the rectangle.

> **Note:** The rectangles **do not overlap**.

### Task
Determine if it is possible to make either **two horizontal or two vertical cuts** on the grid such that:

1. Each of the **three resulting sections** formed by the cuts **contains at least one rectangle**.
2. Every rectangle belongs to **exactly one section**.

Return `true` if such cuts can be made; otherwise, return `false`.

---

## Example 1:

Input: n = 5 rectangles = [[1,0,5,2],[0,2,2,4],[3,2,5,3],[0,4,4,5]]

Output: true


---

## Example 2:


Input: n = 4 rectangles = [[0,0,1,1],[2,0,3,4],[0,2,2,3],[3,0,4,3]]

Output: true


---

## Constraints:
- `1 <= n <= 10⁹`
- `3 <= rectangles.length <= 100`
- `0 <= startx < endx <= n`
- `0 <= starty < endy <= n`
- Rectangles do **not** overlap.

---

## Solution Approach

### **Key Idea**
- Since **rectangles do not overlap**, we can represent them as **intervals** on both the **x-axis** and **y-axis**.
- We check **if there exist at least three non-overlapping segments** along the **x-axis** or **y-axis**.

### **Steps**
1. Convert rectangles into **x-axis** and **y-axis** intervals.
2. Count the **number of merged intervals** along both axes.
3. If **either axis** has **at least 3 non-overlapping segments**, return `True`.

---

## Code:

```python
class Solution:
    def checkValidCuts(self, n: int, rectangles: list[list[int]]) -> bool:
        xs = [(startX, endX) for startX, _, endX, _ in rectangles]
        ys = [(startY, endY) for _, startY, _, endY in rectangles]
        return max(self._countMerged(xs),
                   self._countMerged(ys)) >= 3

    def _countMerged(self, intervals: list[tuple[int, int]]) -> int:
        count = 0
        prevEnd = 0
        for start, end in sorted(intervals):
            if start < prevEnd:
                prevEnd = max(prevEnd, end)
            else:
                prevEnd = end
                count += 1
        return count
```
<h2>Time Complexity</h2>

O(n log n) for sorting the intervals.
O(n) for merging the intervals.
Overall Complexity: O(n log n)

<h2>Space Complexity</h2>

O(n) for storing interval lists.


<h2>Explanation:</h2>

Convert each rectangle into (start, end) intervals for x-axis and y-axis.<br>
Sort intervals and count non-overlapping segments.<br>
If either axis contains at least 3 non-overlapping segments, return True.<br>