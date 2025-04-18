# Problem 38: Count and Say
The **count-and-say** sequence is a sequence of digit strings defined recursively as follows:

- `countAndSay(1) = "1"`
- `countAndSay(n)` is the **run-length encoding (RLE)** of `countAndSay(n - 1)`

Run-length encoding is a string compression technique where consecutive identical digits are replaced by the **number of occurrences followed by the digit**.

### Example:

To compress `"3322251"` using RLE:

- "33" → "23"
- "222" → "32"
- "5" → "15"
- "1" → "11"

So, result = `"23321511"`

---

## 🔍 Examples

### Example 1:

**Input:**  
`n = 4`

**Output:**  
`"1211"`

**Explanation:**

countAndSay(1) = "1" countAndSay(2) = "11" countAndSay(3) = "21" countAndSay(4) = "1211"

### Example 2:

**Input:**  
`n = 1`

**Output:**  
`"1"`

---

## ✅ Constraints

- `1 <= n <= 30`

---

## 💡 Follow-Up

Can you implement it **iteratively** instead of recursively?

---

## 💻 Solution (Python)

```python
class Solution:
  def countAndSay(self, n: int) -> str:
    ans = '1'
    for _ in range(n - 1):
      nxt = ''
      i = 0
      while i < len(ans):
        count = 1
        while i + 1 < len(ans) and ans[i] == ans[i + 1]:
          count += 1
          i += 1
        nxt += str(count) + ans[i]
        i += 1
      ans = nxt
    return ans
```
<h2>Time Complexity:</h2>
O(n × m) where n is the number of iterations and m is the average length of the string at each step.<br>
<h2>Space Complexity:</h2>
O(m) for building the new string at each step.<br>
