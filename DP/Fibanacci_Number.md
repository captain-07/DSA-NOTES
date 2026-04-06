---
created: 2026-04-06
revisions:
  - 2026-04-08
  - 2026-04-13
  - 2026-04-21
  - 2026-05-06
---

# Fibonacci Number

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Google #Microsoft #Meta #Apple #TCS

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #recursion [[Recursion]], #dynamicprogramming [[Dynamic Programming]], #math [[Mathematics]]

## Pattern

Recursion → Memoization → Iterative DP (Space Optimization)

---
## Difficulty

Easy  
#easy

---

## ⚡ Key Idea (Core Insight)

The sequence follows $F(n) = F(n-1) + F(n-2)$ with base cases $F(0)=0, F(1)=1$. The most efficient approach avoids redundant calculations by storing only the last two values instead of the entire sequence.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Slide two variables `a` and `b` forward: `a, b = b, a + b`. Repeat $n$ times.

---

## Approach

### Brute Force
- Plain Recursion: `return fib(n-1) + fib(n-2)`.
- Time Complexity: $O(2^n)$ due to overlapping subproblems.

### Better
- **Memoization (Top-Down):** Use a hashmap/array to store results of `fib(i)` to avoid re-computation.
- **Tabulation (Bottom-Up):** Fill an array from $2$ to $n$.
- Time: $O(n)$, Space: $O(n)$.

### Optimal (Space Optimized)
- Use two variables, `prev2` and `prev1`, to track $F(n-2)$ and $F(n-1)$.
- Iterate from $2$ to $n$, updating variables in each step.
- Time: $O(n)$, Space: $O(1)$.

---

## Code (Python)

```python
def fib(n: int) -> int:
    # Base cases
    if n <= 1:
        return n
    
    # prev2 is F(n-2), prev1 is F(n-1)
    prev2, prev1 = 0, 1
    
    for _ in range(2, n + 1):
        # Current F(n) = F(n-1) + F(n-2)
        current = prev1 + prev2
        # Update pointers for next iteration
        prev2 = prev1
        prev1 = current
        
    return prev1
```

---

## Dry Run (Smart Example)

Input: `n = 4`

| Step | prev2 | prev1 | current | Explanation |
| :--- | :--- | :--- | :--- | :--- |
| Init | 0 | 1 | - | Base cases $F(0), F(1)$ |
| $i=2$ | 1 | 1 | 1 | $0 + 1 = 1$; shift pointers |
| $i=3$ | 1 | 2 | 2 | $1 + 1 = 2$; shift pointers |
| $i=4$ | 2 | 3 | 3 | $1 + 2 = 3$; final result |

Result: **3**

---

## Edge Cases

- **n = 0:** Should return 0 immediately.
- **n = 1:** Should return 1 immediately.
- **Large n:** Python handles large integers automatically, but consider overflow in other languages.

---

## Mistakes

- **Recalculating:** Using pure recursion without memoization in an interview.
- **Off-by-one:** Starting the loop at the wrong index or returning the wrong variable.
- **Space Waste:** Using an $O(n)$ array when only the last two values are needed.
- **User Mistake:** No specific note provided.

---

## Complexity

Time: $O(n)$ → We iterate from $2$ to $n$ exactly once.  
Space: $O(1)$ → Only two variables used regardless of input size.

---

## Tags and Properties
- #dsa #important #revisit #basics
- [[Dynamic Programming]] [[Recursion]] [[Fibonacci]]
- Revision Date: 2026-04-06
- Related: [[Climbing Stairs]], [[House Robber]]

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-08)
- [ ] Day 7 Revision (2026-04-13)
- [ ] Day 15 Revision (2026-04-21)
- [ ] Day 30 Revision (2026-05-06)
