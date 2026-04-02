---
created: 2026-04-02
revisions:
  - 2026-04-04
  - 2026-04-09
  - 2026-04-17
  - 2026-05-02
---

# Print All Divisors

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Microsoft #GoldmanSachs #TCS #Infosys

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #math [[Mathematics]]
  - #divisors [[Number Theory]]
  - #sqrt-optimization [[Square Root Optimization]]

## Pattern
Square Root Decomposition (Math)

---
## Difficulty
Easy #easy

---

## ⚡ Key Idea (Core Insight)
Divisors always exist in pairs. If $i$ is a divisor of $n$, then $n/i$ is also a divisor. For any number $n$, at least one divisor in every pair must be less than or equal to $\sqrt{n}$. This allows us to reduce the search space from $O(n)$ to $O(\sqrt{n})$.

---

## ⚡ Quick Recall (VERY IMPORTANT)
Iterate from $1$ to $\sqrt{n}$. If $i$ divides $n$, collect both $i$ and $n/i$ (ensuring they aren't the same for perfect squares).

---

## Approach

### Brute Force
- Iterate from $1$ to $n$ and check if $n \% i == 0$.
- Time Complexity: $O(n)$

### Optimal
- Iterate from $1$ to $\sqrt{n}$. 
- If $i$ divides $n$, then $i$ is a divisor.
- If $(n / i) \neq i$, then $n / i$ is also a divisor.
- Time Complexity: $O(\sqrt{n})$

---

## Code (Python)

```python
import math

def print_divisors(n):
    divisors = []
    # Loop from 1 to sqrt(n)
    for i in range(1, int(math.sqrt(n)) + 1):
        if n % i == 0:
            divisors.append(i)
            # Add the pair divisor if it's different
            if i != n // i:
                divisors.append(n // i)
    
    # Sorting is optional based on problem requirements
    return sorted(divisors)

# Example usage:
# print(print_divisors(36))
```

---

## Dry Run (Smart Example)

**Input:** $n = 36$

| Step | $i$ | $36 \% i == 0$ | Divisors Found | Explanation |
| :--- | :--- | :--- | :--- | :--- |
| 1 | 1 | Yes | [1, 36] | $36/1 = 36$. Both added. |
| 2 | 2 | Yes | [1, 36, 2, 18] | $36/2 = 18$. Both added. |
| 3 | 3 | Yes | [1, 36, 2, 18, 3, 12] | $36/3 = 12$. Both added. |
| 4 | 4 | Yes | [1, 36, 2, 18, 3, 12, 4, 9] | $36/4 = 9$. Both added. |
| 5 | 5 | No | - | No action. |
| 6 | 6 | Yes | [..., 6] | $36/6 = 6$. Only one 6 added (prevents duplicate). |

---

## Edge Cases

- **$n = 1$:** Should return `[1]`.
- **Prime Numbers ($n = 7$):** Should return `[1, 7]`.
- **Perfect Squares ($n = 25$):** Ensure the square root (5) is not added twice.
- **Large $n$:** $O(\sqrt{n})$ handles large inputs where $O(n)$ would Time Limit Exceeded (TLE).

---

## Mistakes

- **User Mistake:** No specific note provided.
- **Complexity Trap:** Iterating up to $n$ instead of $\sqrt{n}$ for large inputs.
- **Perfect Square Bug:** Forgetting the `if i != n // i` check, resulting in duplicate divisors (e.g., adding `6` twice for `36`).
- **Formatting:** Returning divisors in unsorted order when the problem expects sorted output.

---

## Complexity

Time: $O(\sqrt{n})$ → We only iterate up to the square root of $n$.  
Space: $O(d)$ → Where $d$ is the number of divisors stored in the list.

---

## Tags and Properties
- #dsa #important #revisit #basic-math
- [[Mathematics]] [[Number Theory]] [[Optimization]]
- Revision Date: 2026-04-02
- Status: Completed

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-04)
- [ ] Day 7 Revision (2026-04-09)
- [ ] Day 15 Revision (2026-04-17)
- [ ] Day 30 Revision (2026-05-02)
