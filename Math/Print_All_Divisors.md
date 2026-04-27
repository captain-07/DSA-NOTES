---
created: 2026-04-07
revisions:
  - 2026-04-09
  - 2026-04-14
  - 2026-04-22
  - 2026-05-07
---

# Print All Divisors

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Microsoft #Google #TCS #Adobe #GoldmanSachs

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #math [[Math]], #number-theory [[Number Theory]]

## Pattern

Square Root Property (Divisor Pairing)

---
## Difficulty

Easy #easy

---

## ⚡ Key Idea (Core Insight)

Divisors always occur in pairs. If $i$ is a divisor of $n$, then $n/i$ is also a divisor. One of these factors must be less than or equal to $\sqrt{n}$. By iterating only up to $\sqrt{n}$, we can find all divisors efficiently.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Iterate from $1$ to $\sqrt{n}$. If $n \% i == 0$, $i$ is a divisor. Add $n//i$ as the second divisor only if $i \times i \neq n$ (to avoid duplicates in perfect squares).

---

## Approach

### Brute Force
- Iterate from $1$ to $n$ and check if $n \% i == 0$.
- **Time Complexity:** $O(n)$

### Optimal
- Iterate from $1$ up to $\lfloor\sqrt{n}\rfloor$.
- For every $i$ that divides $n$, the pair $(i, n/i)$ gives two divisors.
- Special handling for perfect squares: if $i = n/i$, count it only once.
- **Time Complexity:** $O(\sqrt{n})$

---

## Code (Python)

```python
import math

def get_all_divisors(n):
    # List to store divisors
    divisors = []
    
    # Iterate from 1 to sqrt(n)
    for i in range(1, int(math.sqrt(n)) + 1):
        if n % i == 0:
            # i is a divisor
            divisors.append(i)
            
            # n // i is the paired divisor
            # Check if it's different from i (handle perfect squares)
            if i * i != n:
                divisors.append(n // i)
                
    # Sort for standard output (optional, depends on requirement)
    divisors.sort()
    return divisors

# Example Usage
print(get_all_divisors(36))
```

---

## Dry Run (Smart Example)

**Input:** $n = 36$ (Perfect Square)

| Step | $i$ | $n \% i$ | Variables / Action | Explanation |
| :--- | :--- | :--- | :--- | :--- |
| 1 | 1 | 0 | `divs = [1, 36]` | $1 \times 36 = 36$. Add both. |
| 2 | 2 | 0 | `divs = [1, 36, 2, 18]` | $2 \times 18 = 36$. Add both. |
| 3 | 3 | 0 | `divs = [1, 36, 2, 18, 3, 12]` | $3 \times 12 = 36$. Add both. |
| 4 | 4 | 0 | `divs = [1, ..., 4, 9]` | $4 \times 9 = 36$. Add both. |
| 5 | 5 | 1 | No change | 5 does not divide 36. |
| 6 | 6 | 0 | `divs = [..., 6]` | $6 \times 6 = 36$. $i = n/i$, add once. |

---

## Edge Cases

- **$n = 1$:** Only one divisor [1].
- **Perfect Square ($n = 16, 25, 36$):** Ensure the square root is not added twice.
- **Prime Number ($n = 13$):** Should return only [1, 13].
- **Large Prime:** Loop still runs $O(\sqrt{n})$ even if only 2 divisors exist.

---

## Mistakes

- **$O(n)$ implementation:** Using a linear loop for large $n$ (e.g., $10^9$) will TLE.
- **Duplicate $\sqrt{n}$:** Forgetting to check `i * i != n` before adding the paired divisor.
- **Missing $1$ or $n$:** Ensure the loop starts at 1 and includes the pairing logic for $n$.
- **User Mistake:** No specific note provided.

---

## Complexity

Time: $O(\sqrt{n})$ → The loop runs from 1 to the square root of $n$. Sorting takes $O(D \log D)$ where $D$ is the number of divisors.  
Space: $O(D)$ → Storing all divisors in a list, where $D$ is the total count of divisors.

---

## Similar Problems

- [Number of Factors](https://www.geeksforgeeks.org/problems/number-of-factors1435/1) - Easy
- [Sum of All Divisors](https://www.geeksforgeeks.org/problems/sum-of-all-divisors-from-1-to-n4738/1) - Easy
- [Check for Prime](https://leetcode.com/problems/prime-arrangements/) - Easy
- [Perfect Number](https://leetcode.com/problems/perfect-number/) - Easy

---

## Tags and Properties
- #dsa #important #revisit #math #divisors
- [[Math]] [[Number Theory]]
- **Revision Date:** 2026-04-07
- **Problem Link:** [GeeksforGeeks - All Divisors of a Number](https://www.geeksforgeeks.org/problems/all-divisors-of-a-number/1)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-09)
- [ ] Day 7 Revision (2026-04-14)
- [ ] Day 15 Revision (2026-04-22)
- [ ] Day 30 Revision (2026-05-07)
