# Problem 1534: Count Good Triplets

Given an array of integers `arr`, and three integers `a`, `b`, and `c`, your task is to find the number of **good triplets**.

---

## ✅ A triplet (arr[i], arr[j], arr[k]) is considered good if:

- `0 <= i < j < k < arr.length`
- `|arr[i] - arr[j]| <= a`
- `|arr[j] - arr[k]| <= b`
- `|arr[i] - arr[k]| <= c`

Where `|x|` denotes the **absolute value** of `x`.

---

## 🔍 Examples

### Example 1:

Input: arr = [3,0,1,1,9,7], a = 7, b = 2, c = 3
Output: 4

**Explanation:**  
Valid good triplets are:  
- (3,0,1)
- (3,0,1)
- (3,1,1)
- (0,1,1)

---

### Example 2:


Input: arr = [1,1,2,2,3], a = 0, b = 0, c = 1
Output: 0

**Explanation:**  
No triplet satisfies all conditions.

---

## 🔐 Constraints

- `3 <= arr.length <= 100`
- `0 <= arr[i] <= 1000`
- `0 <= a, b, c <= 1000`

---

## 💡 Approach

We check **all combinations of three distinct indices (i, j, k)** where `i < j < k` using `itertools.combinations`.

For each triplet, we check the 3 given conditions. If all are satisfied, we count it as a **good triplet**.

---

## 🧪 Python Code

```python
import itertools

class Solution:
  def countGoodTriplets(self, arr: list[int], a: int, b: int, c: int) -> int:
    return sum(
      abs(arr[i] - arr[j]) <= a and
      abs(arr[j] - arr[k]) <= b and
      abs(arr[i] - arr[k]) <= c
      for i, j, k in itertools.combinations(range(len(arr)), 3)
    )
```
<h2>Time Complexity</h2>

O(n^3) where n is the length of the array. But feasible for n <= 100.<br>
<h2>Space Complexity</h2>

O(1) extra space (aside from the input and output).<br>

