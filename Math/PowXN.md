---
created: 2026-06-06
revisions:
  - 2026-06-08
  - 2026-06-13
  - 2026-06-21
  - 2026-07-06
---

# Pow(X, N)

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Google #Microsoft #Facebook #Bloomberg #LinkedIn

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #math [[Mathematics]], #recursion [[Recursion]], #binary-exponentiation [[Binary Exponentiation]]

## Pattern

Binary Exponentiation (Exponentiation by Squaring)  
Divide and Conquer  

---
## Difficulty

Medium  
#medium

---

## ⚡ Key Idea (Core Insight)

The naive $O(N)$ multiplication is too slow. Use the property $x^n = (x^2)^{n/2}$ for even $n$, and $x \cdot x^{n-1}$ for odd $n$. This reduces the number of multiplications to $O(\log N)$ by halving the exponent at each step.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Square the base and halve the exponent. If the exponent is odd, multiply the result by the current base once before continuing.

---

## Approach

### Brute Force
- Multiply $x$ by itself $n$ times using a loop.
- Time: $O(n)$

### Better (Recursive)
- Use recursion: `f(x, n) = f(x*x, n//2)`. Handle $n < 0$ by using $1/x$ and $-n$.
- Time: $O(\log n)$, Space: $O(\log n)$ due to recursion stack.

### Optimal (Iterative)
- Use a `while n > 0` loop.
- If $n$ is odd, multiply `ans` by `x`.
- Always square `x` and integer-divide `n` by 2 in each iteration.
- Handle negative $n$ by converting $x = 1/x$ and $n = -n$ at the start.

---

## Code (Python)

```python
class Solution:
    def myPow(self, x: float, n: int) -> float:
        # Handle negative exponent
        if n < 0:
            x = 1 / x
            n = -n
        
        res = 1
        current_product = x
        
        while n > 0:
            # If n is odd, multiply res by current_product
            if n % 2 == 1:
                res *= current_product
            
            # Square the base and halve the exponent
            current_product *= current_product
            n //= 2
            
        return res
```

---

## Dry Run (Smart Example)

**Input:** `x = 2.0, n = 10`

| Step | `n` | `current_product` | `res` | Explanation |
| :--- | :--- | :--- | :--- | :--- |
| Start | 10 | 2.0 | 1.0 | Initial state |
| 1 | 5 | 4.0 | 1.0 | $n$ was even: $x \to x^2, n \to n/2$ |
| 2 | 2 | 16.0 | 4.0 | $n$ was odd: $res \times 4.0, x \to x^2, n \to n/2$ |
| 3 | 1 | 256.0 | 4.0 | $n$ was even: $x \to x^2, n \to n/2$ |
| 4 | 0 | 65536.0 | 1024.0 | $n$ was odd: $res \times 256.0$, Loop Ends |

---

## Edge Cases

- **$n = 0$**: Result is always 1.0 (except $0^0$ which is usually 1 in programming).
- **$n < 0$**: Reciprocal the base ($1/x$) and make $n$ positive.
- **$x = 1.0$**: Result is always 1.0 regardless of $n$.
- **$x = 0$**: Result is 0 for $n > 0$; undefined/error for $n < 0$.
- **$n = \text{Min Int}$**: In some languages (C++/Java), $-n$ overflows; Python handles this automatically.

---

## Mistakes

- **Forgetting Negative Exponents**: Must handle $x^{-n} = (1/x)^n$.
- **Linear Complexity**: Using a simple loop results in TLE for large $n$.
- **Integer Division**: Using `/` instead of `//` in Python for $n$.
- **User Mistake**: No specific note provided.

---

## Complexity

Time: $O(\log n)$ → The exponent $n$ is halved in every iteration of the loop.  
Space: $O(1)$ → Iterative approach uses a constant amount of extra space.

---

## Similar Problems

- [Sqrt(x)](https://leetcode.com/problems/sqrtx/) - Easy
- [Super Pow](https://leetcode.com/problems/super-pow/) - Medium
- [Count Good Numbers](https://leetcode.com/problems/count-good-numbers/) - Medium

---

## Tags and Properties
  - #dsa #important #revisit  
  - #binary-exponentiation #math #fast-power
  - [[Binary Exponentiation]] [[Recursion]] [[Divide and Conquer]]
  - **Problem Link:** [LeetCode - Pow(x, n)](https://leetcode.com/problems/powx-n/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-06-08)
- [ ] Day 7 Revision (2026-06-13)
- [ ] Day 15 Revision (2026-06-21)
- [ ] Day 30 Revision (2026-07-06)
