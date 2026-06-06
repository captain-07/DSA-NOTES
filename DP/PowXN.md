---
created: 2026-06-06
revisions:
  - 2026-06-08
  - 2026-06-13
  - 2026-06-21
  - 2026-07-06
---

# Pow(X,N)

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Google #Facebook #Amazon #LinkedIn #Bloomberg #Microsoft

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #binaryexponentiation [[Binary Exponentiation]]
  - #divideandconquer [[Divide and Conquer]]
  - #recursion [[Recursion]]
  - #bitmanipulation [[Bit Manipulation]]

---
## Pattern

Binary Exponentiation (Divide and Conquer)

---
## Difficulty

Medium #medium

---

## ⚡ Key Idea (Core Insight)

The core insight is **Binary Exponentiation**: reduce the number of multiplications from $O(n)$ to $O(\log n)$ by observing that $x^n = (x^2)^{n/2}$ if $n$ is even, and $x^n = x \cdot (x^2)^{(n-1)/2}$ if $n$ is odd.

---

## ⚡ Quick Recall (VERY IMPORTANT)

**Halve the power, square the base.** If $n$ is odd, multiply the result by the current base once. Handle negative $n$ by using $1/x$ and $-n$.

---

## Approach

### Brute Force
- Multiply $x$ by itself $n$ times using a loop.
- Time Complexity: $O(n)$
- Space Complexity: $O(1)$

### Better (Recursive)
- Use recursion to compute `half = pow(x, n // 2)`.
- If $n$ is even, return `half * half`. If odd, return `x * half * half`.
- Time Complexity: $O(\log n)$
- Space Complexity: $O(\log n)$ due to recursion stack.

### Optimal (Iterative)
- Use a loop while $n > 0$. 
- If $n$ is odd, multiply `ans` by `x`. 
- Square `x` and halve `n` (using integer division or bit shift) in every step.
- Time Complexity: $O(\log n)$
- Space Complexity: $O(1)$

---

## Code (Python)

```python
class Solution:
    def myPow(self, x: float, n: int) -> float:
        # Handle negative exponent
        if n < 0:
            x = 1 / x
            n = -n
        
        ans = 1.0
        current_product = x
        
        while n > 0:
            # If n is odd, multiply the result by current_product
            if n % 2 == 1:
                ans *= current_product
            
            # Square the base and halve the exponent
            current_product *= current_product
            n //= 2
            
        return ans
```

---

## Dry Run (Smart Example)

**Input:** `x = 2.0`, `n = 10`

| Step | n | x (current_product) | ans | Explanation |
| :--- | :--- | :--- | :--- | :--- |
| 1 | 10 | 2.0 | 1.0 | $n$ is even. $x = 2.0^2 = 4.0$, $n = 10//2 = 5$. |
| 2 | 5 | 4.0 | 4.0 | $n$ is odd. $ans = 1.0 \times 4.0 = 4.0$, $x = 4.0^2 = 16.0$, $n = 5//2 = 2$. |
| 3 | 2 | 16.0 | 4.0 | $n$ is even. $x = 16.0^2 = 256.0$, $n = 2//2 = 1$. |
| 4 | 1 | 256.0 | 1024.0 | $n$ is odd. $ans = 4.0 \times 256.0 = 1024.0$, $n = 1//2 = 0$. |

---

## Edge Cases

- **$n = 0$:** Always returns $1.0$.
- **$n < 0$:** Compute $(1/x)^{-n}$. Note: In some languages (C++), $-(-2^{31})$ overflows; Python handles this automatically.
- **$x = 0$:** $0^n$ is $0$ (for $n > 0$), but $0^0$ is usually $1$.
- **$x = 1$ or $x = -1$:** Result cycles between $1$ and $-1$.
- **Large $n$:** $O(\log n)$ is essential to avoid TLE.

---

## Mistakes

- **Linear multiplication:** Using $O(n)$ loop results in Time Limit Exceeded (TLE).
- **Ignoring negative $n$:** Forgetting to convert $x$ to $1/x$.
- **Recursion depth:** Recursive approach might hit stack limits for very large $n$ in some environments.
- **User mistake:** No specific note provided (ensure standard structure is followed).

---

## Complexity

Time: $O(\log n)$ → The exponent is halved in each iteration of the loop.  
Space: $O(1)$ → Iterative approach uses only a constant amount of extra space.

---

## Similar Problems

- [Super Pow](https://leetcode.com/problems/super-pow/) - Medium
- [Sqrt(x)](https://leetcode.com/problems/sqrtx/) - Easy
- [Count Good Numbers](https://leetcode.com/problems/count-good-numbers/) - Medium
- [Modular Exponentiation](https://www.geeksforgeeks.org/modular-exponentiation-power-in-modular-arithmetic/) - Medium

---

## Tags and Properties
  - #dsa #important #revisit #math #binary_exponentiation
  - [[Binary Exponentiation]] [[Divide and Conquer]]
  - **Revision Date:** 2026-06-06
  - **Problem Link:** [LeetCode - Pow(x, n)](https://leetcode.com/problems/powx-n/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-06-08)
- [ ] Day 7 Revision (2026-06-13)
- [ ] Day 15 Revision (2026-06-21)
- [ ] Day 30 Revision (2026-07-06)
