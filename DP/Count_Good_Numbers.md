---
created: 2026-06-06
revisions:
  - 2026-06-08
  - 2026-06-13
  - 2026-06-21
  - 2026-07-06
---

# Count Good Numbers

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Google #Microsoft #Adobe #Meta #Apple

- **Confidence Checklist:**
  - [ ] Low  
  - [x] Medium  
  - [ ] High  

- **Concepts:**
  - #math [[Math]]
  - #recursion [[Recursion]]
  - #binaryexponentiation [[Binary Exponentiation]]
  - #combinatorics [[Combinatorics]]

## Pattern

Combinatorics + Modular Exponentiation (Binary Exponentiation)

---
## Difficulty

Medium  
#medium

---

## ⚡ Key Idea (Core Insight)

The problem is a counting problem where choices at each position are independent:
1. **Even Indices (0, 2, 4...)**: Must be an even digit $\{0, 2, 4, 6, 8\} \rightarrow$ **5 choices**.
2. **Odd Indices (1, 3, 5...)**: Must be a prime digit $\{2, 3, 5, 7\} \rightarrow$ **4 choices**.
3. Since $n$ is up to $10^{15}$, we must use **Binary Exponentiation** to calculate $(5^{\text{even\_pos}} \times 4^{\text{odd\_pos}}) \pmod{10^9+7}$ in $O(\log n)$ time.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Result = `(pow(5, (n + 1) // 2, MOD) * pow(4, n // 2, MOD)) % MOD`. Use modular exponentiation for large $n$.

---

## Approach

### Brute Force
- Iterate from $0$ to $10^n - 1$, check if each digit string is "good".
- **Time Complexity:** $O(n \cdot 10^n)$ - Impossible for $n=10^{15}$.

### Better
- Calculate `(5^(even_count) * 4^(odd_count))` using a simple loop.
- **Time Complexity:** $O(n)$ - Still too slow for $10^{15}$.

### Optimal
- **Step 1:** Calculate number of even positions: `even = (n + 1) // 2`.
- **Step 2:** Calculate number of odd positions: `odd = n // 2`.
- **Step 3:** Use Binary Exponentiation (Fast Power) to compute $5^{even} \pmod{MOD}$ and $4^{odd} \pmod{MOD}$.
- **Step 4:** Return the product of both results modulo $10^9 + 7$.

---

## Code (Python)

```python
class Solution:
    def countGoodNumbers(self, n: int) -> int:
        MOD = 10**9 + 7
        
        # Binary Exponentiation function: (base^exp) % mod
        def fast_pow(base, exp):
            res = 1
            base %= MOD
            while exp > 0:
                if exp % 2 == 1:
                    res = (res * base) % MOD
                base = (base * base) % MOD
                exp //= 2
            return res

        # Even positions: 0, 2, 4... (Total: ceil(n/2))
        # Odd positions: 1, 3, 5... (Total: floor(n/2))
        even_pos = (n + 1) // 2
        odd_pos = n // 2
        
        # Choices: 5 for even indices, 4 for odd indices
        return (fast_pow(5, even_pos) * fast_pow(4, odd_pos)) % MOD
```

---

## Dry Run (Smart Example)

Input: `n = 3` (Length 3 digit string)

| Step | Operation | Variables | Explanation |
| :--- | :--- | :--- | :--- |
| 1 | Calculate Positions | `even=2`, `odd=1` | Indices [0, 2] are even, [1] is odd. |
| 2 | Fast Pow (5, 2) | `5^2 = 25` | $5 \times 5 = 25$ choices for even slots. |
| 3 | Fast Pow (4, 1) | `4^1 = 4` | $4$ choices for the odd slot. |
| 4 | Final Product | `(25 * 4) % MOD = 100` | Total 100 good numbers of length 3. |

---

## Edge Cases

- **$n = 1$**: `even=1, odd=0`. Result: $5^1 \times 4^0 = 5$. Correct (0, 2, 4, 6, 8).
- **$n = 10^{15}$**: Requires `log(n)` steps due to large exponent.
- **Modulo Wrap**: Ensure every multiplication step is wrapped in `% MOD` to prevent overflow.

---

## Mistakes

- **Mismatching Choices**: Confusing 5 choices for even and 4 for odd. Remember: Even digits are $\{0,2,4,6,8\}$ (5), Prime digits are $\{2,3,5,7\}$ (4).
- **Linear Power**: Using a loop for power instead of Binary Exponentiation; will TLE (Time Limit Exceeded).
- **User Mistake (dont understand)**: Not realizing that positions are independent. If you have 2 slots and each has 5 choices, total is $5 \times 5 = 5^2$. This is basic combinatorics.

---

## Complexity

Time: $O(\log n)$ → Due to binary exponentiation (fast power) logic.  
Space: $O(1)$ → Constant space used for calculations.

---

## Similar Problems

- [Pow(x, n)](https://leetcode.com/problems/powx-n/) - Medium
- [Super Pow](https://leetcode.com/problems/super-pow/) - Medium
- [Modular Exponentiation](https://www.geeksforgeeks.org/modular-exponentiation-power-in-modular-arithmetic/) - Medium

---

## Tags and Properties
  - #dsa #important #revisit  
  - #combinatorics #binaryexponentiation #math
  - [[Binary Exponentiation]] [[Math]]
  - **Problem Link:** [LeetCode 1922 - Count Good Numbers](https://leetcode.com/problems/count-good-numbers/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-06-08)
- [ ] Day 7 Revision (2026-06-13)
- [ ] Day 15 Revision (2026-06-21)
- [ ] Day 30 Revision (2026-07-06)
