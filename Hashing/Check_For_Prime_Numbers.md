---
created: 2026-04-07
revisions:
  - 2026-04-09
  - 2026-04-14
  - 2026-04-22
  - 2026-05-07
---

MCP issues detected. Run /mcp list for status.# Check For Prime Numbers

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Google #Microsoft #TCS #Infosys #GoldmanSachs

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #math [[Math]]
  - #numbertheory [[Number Theory]]
  - #primality [[Primality Test]]

## Pattern
Trial Division (Square Root Property)

---
## Difficulty
Easy #easy

---

## ⚡ Key Idea (Core Insight)
A number $n$ is prime if it has no divisors other than 1 and itself. If $n = a \times b$, then at least one factor must be less than or equal to $\sqrt{n}$. Testing divisors up to $\sqrt{n}$ is sufficient to prove primality.

---

## ⚡ Quick Recall (VERY IMPORTANT)
Iterate from 2 up to $\sqrt{n}$. If any number divides $n$ evenly, it is not prime. Handle $n \le 1$ as a special case.

---

## Approach

### Brute Force
- Iterate from 2 to $n-1$ and check if $n \% i == 0$.
- **Time Complexity:** $O(n)$

### Optimal (Trial Division)
- Iterate from 2 to $\lfloor \sqrt{n} \rfloor$.
- If $n \% i == 0$ at any point, return `False`.
- **Time Complexity:** $O(\sqrt{n})$

### Highly Optimal ($6k \pm 1$ Optimization)
- Primes greater than 3 follow the $6k \pm 1$ rule.
- Check if $n \le 3$, then check if divisible by 2 or 3.
- Iterate from 5, incrementing by 6 each time, checking $i$ and $i+2$.
- **Time Complexity:** $O(\sqrt{n})$ but with a smaller constant factor (3x faster than basic trial division).

---

## Code (Python)

```python
import math

def is_prime(n):
    # Handle edge cases
    if n <= 1:
        return False
    if n <= 3:
        return True
    
    # Optimization: check 2 and 3
    if n % 2 == 0 or n % 3 == 0:
        return False
    
    # Check factors from 5 to sqrt(n)
    # Every prime > 3 is of the form 6k +/- 1
    limit = int(math.sqrt(n))
    for i in range(5, limit + 1, 6):
        if n % i == 0 or n % (i + 2) == 0:
            return False
            
    return True
```

---

## Dry Run (Smart Example)

**Input:** $n = 25$

| Step | Variables | Explanation |
| :--- | :--- | :--- |
| 1 | $n = 25$ | Initial input. $n > 3$, not divisible by 2 or 3. |
| 2 | `limit` = 5 | Calculated $\sqrt{25} = 5$. |
| 3 | $i = 5$ | Start loop at 5. Check $n \% 5 == 0$. |
| 4 | $25 \% 5 == 0$ | Condition true. Divisor found. |
| 5 | Return `False` | 25 is not a prime number. |

---

## Edge Cases

- **$n = 1$:** Not prime (Definition: Prime > 1).
- **$n = 2$:** Smallest and only even prime.
- **$n = 3$:** Smallest odd prime.
- **Negative numbers:** Not prime.
- **Large Primes (e.g., 10^9 + 7):** Efficiently handled by $\sqrt{n}$ logic.

---

## Mistakes

- Treating 1 as a prime number.
- Forgetting to check divisibility up to $\sqrt{n}$ (inclusive).
- Not handling even numbers or $n \le 0$ correctly.
- **User Mistake:** No specific note provided.

---

## Complexity

- **Time:** $O(\sqrt{n})$ → We only check divisors up to the square root of $n$.
- **Space:** $O(1)$ → No extra data structures used; only constant space for variables.

---

## Similar Problems

- [Count Primes](https://leetcode.com/problems/count-primes/) - Medium
- [Sieve of Eratosthenes](https://www.geeksforgeeks.org/sieve-of-eratosthenes/) - Easy
- [Closest Prime Numbers in Range](https://leetcode.com/problems/closest-prime-numbers-in-range/) - Medium
- [Perfect Number](https://leetcode.com/problems/perfect-number/) - Easy

---

## Tags and Properties
- #dsa #important #revisit #math #primality
- [[Math]] [[Number Theory]]
- **Revision Date:** 2026-04-07
- **Problem Link:** [Primality Test - GeeksforGeeks](https://www.geeksforgeeks.org/primality-test-set-1-introduction-and-school-method/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-09)
- [ ] Day 7 Revision (2026-04-14)
- [ ] Day 15 Revision (2026-04-22)
- [ ] Day 30 Revision (2026-05-07)
