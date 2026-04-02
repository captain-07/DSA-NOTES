---
created: 2026-04-02
revisions:
  - 2026-04-04
  - 2026-04-09
  - 2026-04-17
  - 2026-05-02
---

# Gcd Of Two Numbers

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Microsoft #Google #TCS #Adobe #Oracle

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #math [[Math]]
  - #recursion [[Recursion]]
  - #number-theory [[Number Theory]]

---
## Pattern

Euclidean Algorithm (Modulo Version)

---
## Difficulty

Easy 
#easy

---

## ⚡ Key Idea (Core Insight)

The Greatest Common Divisor (GCD) of two numbers $a$ and $b$ remains the same if the larger number is replaced by its remainder when divided by the smaller number.  
**Property:** $gcd(a, b) = gcd(b, a \pmod b)$ until $b$ becomes $0$.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Repeatedly apply `a, b = b, a % b` until `b` is `0`. The answer is `a`.

---

## Approach

### Brute Force
- Iterate from `min(a, b)` down to 1. The first number that divides both $a$ and $b$ is the GCD.
- **Time Complexity:** $O(\min(a, b))$

### Better (Basic Euclidean)
- Repeatedly subtract the smaller number from the larger number until they become equal.
- **Time Complexity:** $O(\max(a, b))$ in worst case (e.g., $gcd(10^9, 1)$).

### Optimal (Optimized Euclidean)
- Use the **Modulo operator** to jump multiple subtractions.
- If $b > 0$, calculate $a \pmod b$ and recurse.
- Base case: If $b = 0$, return $a$.

---

## Code (Python)

```python
def get_gcd(a, b):
    # Base Case: if b is 0, a is the GCD
    while b:
        # Update a to b, and b to the remainder of a/b
        a, b = b, a % b
    return a

# Alternative Recursive Version
def gcd_recursive(a, b):
    return a if b == 0 else gcd_recursive(b, a % b)
```

---

## Dry Run (Smart Example)

**Input:** $a = 48, b = 18$

| Step | a | b | Explanation |
| :--- | :--- | :--- | :--- |
| 1 | 48 | 18 | Initial values. $b \neq 0$, so calculate $48 \pmod{18}$. |
| 2 | 18 | 12 | $a$ becomes old $b$ ($18$), $b$ becomes $48 \pmod{18} = 12$. |
| 3 | 12 | 6 | $a$ becomes old $b$ ($12$), $b$ becomes $18 \pmod{12} = 6$. |
| 4 | 6 | 0 | $a$ becomes old $b$ ($6$), $b$ becomes $12 \pmod 6 = 0$. |
| 5 | **6** | - | $b$ is $0$. Return $a = 6$. |

---

## Edge Cases

- **One number is 0:** `gcd(a, 0)` is $a$.
- **Both numbers are equal:** `gcd(a, a)` is $a$.
- **One number is 1:** GCD is always 1.
- **Prime Numbers:** `gcd(7, 13)` is 1.

---

## Mistakes

- **Subtraction vs Modulo:** Using `a - b` instead of `a % b` leads to $O(N)$ instead of $O(\log N)$.
- **Base Case:** Forgetting to handle the $b=0$ case in recursion.
- **Euclidean Algo Confusion:** Mixing up the order; always remember the remainder becomes the new divisor ($b$).
- **Negative numbers:** GCD is typically defined as positive; use `abs(a)` and `abs(b)`.

---

## Complexity

Time: $O(\log(\min(a, b)))$ → The numbers decrease exponentially in each step.  
Space: $O(1)$ → For iterative; $O(\log(\min(a, b)))$ for recursion stack.

---

## Tags and Properties
  - #dsa #important #revisit  
  - #gcd #euclidean-algorithm #math-fundamentals
  - [[Math]] [[Euclidean Algorithm]]
  - Last Revised: 2026-04-02

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-04)
- [ ] Day 7 Revision (2026-04-09)
- [ ] Day 15 Revision (2026-04-17)
- [ ] Day 30 Revision (2026-05-02)
