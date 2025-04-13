# Problem 1922: Count Good Numbers

A digit string is considered **good** if:
- Digits at **even indices** (0-based) are **even**: {0, 2, 4, 6, 8}
- Digits at **odd indices** are **prime**: {2, 3, 5, 7}

---

## 📘 Examples

### Example 1:

Input: n = 1
Output: 5

**Explanation:**  
Only the even digits are allowed at position 0: `"0", "2", "4", "6", "8"`

---

### Example 2:


Input: n = 4
Output: 400

**Explanation:**  
Even indices (0, 2): 5 choices each → `5 * 5`  
Odd indices (1, 3): 4 choices each → `4 * 4`  
Total: `5^2 * 4^2 = 25 * 16 = 400`

---

### Example 3:


Input: n = 50
Output: 564908303


---

## 🧠 Approach

- Even indices have **5 options** (even digits)
- Odd indices have **4 options** (prime digits)

For a number of length `n`, we have:
- `ceil(n / 2)` even indices → `5^(n//2 + n%2)`
- `floor(n / 2)` odd indices → `4^(n//2)`

We compute:

count = 5^(ceil(n/2)) * 4^(floor(n/2)) mod (10^9 + 7)


To efficiently compute large powers (since `n` can be up to 10¹⁵), we use **modular exponentiation**.

---

## 🔐 Constraints

- `1 <= n <= 10^15`

---

## 🧪 Python Code

```python
class Solution:
  def countGoodNumbers(self, n: int) -> int:
    MOD = 1_000_000_007

    def modPow(x: int, n: int) -> int:
      if n == 0:
        return 1
      if n % 2 == 1:
        return x * modPow(x, n - 1) % MOD
      return modPow(x * x % MOD, n // 2)

    return modPow(4 * 5, n // 2) * (1 if n % 2 == 0 else 5) % MOD
```
<h2>Time Complexity</h2>
O(log n) for modular exponentiation<br>
</h2> Space Complexity</h2>
O(log n) recursion stack for modPow<br>




