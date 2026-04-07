---
created: 2026-04-07
revisions:
  - 2026-04-09
  - 2026-04-14
  - 2026-04-22
  - 2026-05-07
---

# Fibonacci Number

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Google #Microsoft #Meta #Apple #Adobe

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #dynamicprogramming [[Dynamic Programming]], #recursion [[Recursion]], #math [[Math]]

## Pattern

Recursion + Memoization  
Iterative DP (Space Optimized)

---
## Difficulty

Easy  
#easy

---

## ⚡ Key Idea (Core Insight)

- The sequence follows the recurrence relation $F(n) = F(n-1) + F(n-2)$.
- Instead of recomputing the same subproblems, store previous results (Memoization) or build bottom-up (Tabulation).

---

## ⚡ Quick Recall (VERY IMPORTANT)

- Sum of the previous two numbers; optimize space by using only two variables ($prev1, prev2$) instead of an array.

---

## Approach

### Brute Force
- Simple recursion: `return fib(n-1) + fib(n-2)`.
- Time Complexity: $O(2^n)$ due to redundant calculations.

### Better
- **Memoization (Top-Down):** Use a hash map or array to store results of `fib(n)`.
- **Tabulation (Bottom-Up):** Use an array of size $n+1$ to store results from $0$ to $n$.
- Time: $O(n)$, Space: $O(n)$.

### Optimal (Space Optimized DP)
- Only the last two values are needed to calculate the current value.
- Maintain two variables `a` and `b` to represent $F(i-2)$ and $F(i-1)$.
- Time: $O(n)$, Space: $O(1)$.

---

## Code (Python)

```python
def fib(n: int) -> int:
    # Base cases
    if n <= 1:
        return n
    
    # prev2 is F(i-2), prev1 is F(i-1)
    prev2, prev1 = 0, 1
    
    for i in range(2, n + 1):
        # Current F(i) = F(i-1) + F(i-2)
        current = prev1 + prev2
        # Update pointers for next iteration
        prev2 = prev1
        prev1 = current
        
    return prev1
```

---

## Dry Run (Smart Example)

Input: `n = 4`

| Step | i | prev2 | prev1 | current | Explanation |
| :--- | :--- | :--- | :--- | :--- | :--- |
| Init | - | 0 | 1 | - | Initial base values for F(0) and F(1). |
| 1 | 2 | 1 | 1 | 1 | `current = 0 + 1`. prev2 becomes 1, prev1 becomes 1. |
| 2 | 3 | 1 | 2 | 2 | `current = 1 + 1`. prev2 becomes 1, prev1 becomes 2. |
| 3 | 4 | 2 | 3 | 3 | `current = 2 + 1`. prev2 becomes 2, prev1 becomes 3. |

---

## Edge Cases

- **n = 0:** Should return 0 (Base case).
- **n = 1:** Should return 1 (Base case).
- **Large n:** Python handles large integers automatically, but $O(n)$ time remains efficient.

---

## Mistakes

- **Incorrect Base Case:** Forgetting that $F(0)=0$ and $F(1)=1$.
- **Redundant Work:** Using recursion without memoization (leads to TLE).
- **Suboptimal Space:** Using an $O(n)$ array when only two variables are needed.
- **User Mistake:** No specific note provided.

---

## Complexity

Time: $O(n)$ → We iterate from 2 to $n$ exactly once.  
Space: $O(1)$ → We only store two variables regardless of $n$.

---

## Similar Problems

- [Climbing Stairs](https://leetcode.com/problems/climbing-stairs/) - Easy
- [N-th Tribonacci Number](https://leetcode.com/problems/n-th-tribonacci-number/) - Easy
- [House Robber](https://leetcode.com/problems/house-robber/) - Medium

---

## Tags and Properties
  - #dsa #important #revisit #fibonacci #math
  - [[Dynamic Programming]] [[Recursion]]
  - **Revision Date:** 2026-04-07
  - **Problem Link:** [LeetCode - Fibonacci Number](https://leetcode.com/problems/fibonacci-number/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-09)
- [ ] Day 7 Revision (2026-04-14)
- [ ] Day 15 Revision (2026-04-22)
- [ ] Day 30 Revision (2026-05-07)
