---
created: 2026-04-10
revisions:
  - 2026-04-12
  - 2026-04-17
  - 2026-04-25
  - 2026-05-10
---

# Print All Divisors

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Microsoft #TCS #Infosys #GoldmanSachs

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #mathematics [[Mathematics]], #numbertheory [[Number Theory]], #squareroot [[Square Root Optimization]]

## Pattern

Square Root Optimization ($O(\sqrt{N})$)

---
## Difficulty

Easy #easy

---

## ⚡ Key Idea (Core Insight)

Divisors always occur in pairs. If $d$ is a divisor of $n$, then $n/d$ is also a divisor. By iterating only up to $\sqrt{n}$, we can identify both members of the pair simultaneously, reducing the search space from linear to sub-linear.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Iterate from $1$ to $\sqrt{n}$. If $n \% i == 0$, then $i$ and $n/i$ are both divisors. Use a set or handle the case where $i == n/i$ (perfect squares) to avoid duplicates.

---

## Approach

### Brute Force
- Iterate through all numbers from $1$ to $n$. Check if $n \% i == 0$.
- **Complexity:** $O(n)$ Time, $O(d)$ Space (where $d$ is number of divisors).

### Optimal
- Iterate from $1$ up to $\lfloor\sqrt{n}\rfloor$.
- For each $i$, if $n \% i == 0$:
  1. Add $i$ to the list.
  2. If $n/i \neq i$, add $n/i$ to the list.
- **Complexity:** $O(\sqrt{n})$ Time, $O(d)$ Space.

---

## Code (Python)

```python
import math

class Solution:
    def print_divisors(self, n: int) -> list[int]:
        """
        Returns a sorted list of all divisors of n.
        Uses O(sqrt(n)) optimization.
        """
        divisors = []
        # Iterate up to square root of n
        for i in range(1, int(math.sqrt(n)) + 1):
            if n % i == 0:
                divisors.append(i)
                # If the quotient is different from the divisor, add it
                if i != n // i:
                    divisors.append(n // i)
        
        # Return sorted for consistency
        return sorted(divisors)
```

---

## Dry Run (Smart Example)

**Input:** `n = 36` (Perfect Square)

| Step | $i$ | $n \% i == 0$? | Variables (`divisors`) | Explanation |
| :--- | :--- | :--- | :--- | :--- |
| 1 | 1 | Yes | `[1, 36]` | $36/1 = 36$. Both added. |
| 2 | 2 | Yes | `[1, 36, 2, 18]` | $36/2 = 18$. Both added. |
| 3 | 3 | Yes | `[1, 36, 2, 18, 3, 12]` | $36/3 = 12$. Both added. |
| 4 | 4 | Yes | `[1, 36, 2, 18, 3, 12, 4, 9]` | $36/4 = 9$. Both added. |
| 5 | 5 | No | `[1, 36, 2, 18, 3, 12, 4, 9]` | 5 is not a divisor. |
| 6 | 6 | Yes | `[1, 36, 2, 18, 3, 12, 4, 9, 6]` | $36/6 = 6$. Only 6 added (avoid duplicates). |

---

## Edge Cases

- **$n = 1$:** Only one divisor `[1]`.
- **Prime Numbers ($n = 7$):** Only `[1, 7]`.
- **Perfect Squares ($n = 25$):** Middle divisor $5$ should not be counted twice.
- **Large $n$:** $O(\sqrt{n})$ handles large integers where $O(n)$ would TLE.

---

## Mistakes

- Counting the square root twice for perfect squares.
- Using $O(n)$ loop for large constraints.
- Forgetting that divisors can be stored in any order but often expected sorted.
- **User Mistake:** No specific note provided.

---

## Complexity

Time: $O(\sqrt{n})$ → We only iterate up to the square root of $n$. Sorting the result takes $O(d \log d)$ where $d$ is the number of divisors.  
Space: $O(d)$ → To store the list of divisors.

---

## Similar Problems

- [Count Primes](https://leetcode.com/problems/count-primes/) - Medium
- [Perfect Number](https://leetcode.com/problems/perfect-number/) - Easy
- [Sum of All Divisors](https://www.geeksforgeeks.org/problems/sum-of-all-divisors-from-1-to-n4738/1) - Easy
- [Four Divisors](https://leetcode.com/problems/four-divisors/) - Medium

---

## Tags and Properties
  - #dsa #important #revisit #math #divisors
  - [[Mathematics]] [[Number Theory]]
  - **Revision Date:** 2026-04-10
  - **Problem Link:** [Find all divisors of a natural number](https://www.geeksforgeeks.org/problems/all-divisors-of-a-number/1)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-12)
- [ ] Day 7 Revision (2026-04-17)
- [ ] Day 15 Revision (2026-04-25)
- [ ] Day 30 Revision (2026-05-10)
