---
created: 2026-04-02
revisions:
  - 2026-04-04
  - 2026-04-09
  - 2026-04-17
  - 2026-05-02
---

# Check For Prime Numbers

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Microsoft #Google #TCS #Infosys #Accenture

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #math [[Mathematics]]
  - #numbertheory [[Number Theory]]
  - #algorithms [[Algorithms]]

## Pattern

Trial Division (Square Root Property)

---
## Difficulty

Easy  
#easy

---

## ⚡ Key Idea (Core Insight)

A prime number $n$ has no divisors other than $1$ and itself. If $n$ is composite, it must have at least one factor less than or equal to $\sqrt{n}$. If we find no divisors up to $\sqrt{n}$, $n$ is prime.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Iterate from $2$ to $\text{int}(\sqrt{n}) + 1$. If $n \% i == 0$, return `False`. Special case: numbers $\le 1$ are not prime.

---

## Approach

### Brute Force
- Iterate from $2$ to $n-1$ and check if any number divides $n$.
- **Time Complexity:** $O(n)$

### Better
- Iterate from $2$ to $n/2$. Any factor larger than $n/2$ must have a corresponding factor smaller than $2$ (which doesn't exist for integers).
- **Time Complexity:** $O(n)$

### Optimal
1. Handle base cases: If $n \le 1$, return `False`.
2. Loop from $i = 2$ to $\sqrt{n}$:
   - If $n \pmod i == 0$, return `False`.
3. If loop finishes without finding a divisor, return `True`.

---

## Code (Python)

```python
import math

def is_prime(n):
    # 0 and 1 are not prime numbers
    if n <= 1:
        return False
    
    # Check divisors from 2 up to sqrt(n)
    # Using int(math.sqrt(n)) + 1 for the range limit
    limit = int(math.sqrt(n)) + 1
    for i in range(2, limit):
        if n % i == 0:
            return False # Found a factor, not prime
            
    return True # No factors found, it's prime
```

---

## Dry Run (Smart Example)

**Input:** `n = 25`

| Step | Variable (i) | Calculation | Explanation |
| :--- | :--- | :--- | :--- |
| 1 | - | `n = 25` | Input received. `n > 1` holds. |
| 2 | - | `limit = 6` | `sqrt(25) = 5`. Range is `(2, 6)`. |
| 3 | `i = 2` | `25 % 2 = 1` | Not zero. Continue. |
| 4 | `i = 3` | `25 % 3 = 1` | Not zero. Continue. |
| 5 | `i = 4` | `25 % 4 = 1` | Not zero. Continue. |
| 6 | `i = 5` | `25 % 5 = 0` | **Found factor!** Return `False`. |

---

## Edge Cases

- **n = 1:** Not prime (Definition: Prime > 1).
- **n = 2:** Smallest and only even prime.
- **n = 3:** Prime (loop doesn't run, returns True).
- **Negative numbers:** Always return `False`.
- **Large Square Numbers:** E.g., 121 (11x11), ensures the loop goes up to $\sqrt{n}$ inclusive.

---

## Mistakes

- **Incorrect Boundary:** Running loop until `sqrt(n)` but excluding the actual square root (e.g., missing 5 for 25).
- **Handling 1:** Forgetting that 1 is neither prime nor composite.
- **Even Numbers:** Not optimizing for even numbers (can check `n == 2` then skip all even `i`).
- **User Mistake:** No specific note provided.

---

## Complexity

Time: $O(\sqrt{n})$ → We only check divisors up to the square root of the number.  
Space: $O(1)$ → Constant space used for variables regardless of input size.

---

## Tags and Properties
  - #dsa #important #revisit #prime
  - [[Mathematics]] [[Trial Division]]
  - Revision Date: 2026-04-02
  - Resource: [[Number Theory Basics]]

---

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-04)
- [ ] Day 7 Revision (2026-04-09)
- [ ] Day 15 Revision (2026-04-17)
- [ ] Day 30 Revision (2026-05-02)
