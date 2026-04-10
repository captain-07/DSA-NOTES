---
created: 2026-04-10
revisions:
  - 2026-04-12
  - 2026-04-17
  - 2026-04-25
  - 2026-05-10
---

# Fibonacci Number

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Google #Microsoft #Apple #Adobe #Meta

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #recursion [[Recursion]], #dynamicprogramming [[Dynamic Programming]], #memoization [[Memoization]]

## Pattern

Dynamic Programming (Bottom-Up) + Space Optimization

---
## Difficulty

Easy #easy

---

## ⚡ Key Idea (Core Insight)

The value at `n` is strictly the sum of the two preceding values. Instead of recalculating the entire tree (recursion), we only need to track the **last two states** to compute the current one.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Iterate from 2 to `n`, maintaining `prev1` and `prev2`. Update: `new_val = prev1 + prev2`, then slide the window forward.

---

## Approach

### Brute Force
- Plain Recursion: `return fib(n-1) + fib(n-2)`.
- **Time:** $O(2^n)$ due to massive redundant subproblems.
- **Space:** $O(n)$ recursion stack.

### Better
- Memoization (Top-Down): Store results of `fib(i)` in a hashmap/array.
- **Time:** $O(n)$.
- **Space:** $O(n)$ for the memo table + $O(n)$ stack.

### Optimal
- Iterative Space Optimization (Bottom-Up).
- Use two variables to store $F(n-1)$ and $F(n-2)$ to avoid $O(n)$ space.

---

## Code (Python)

```python
class Solution:
    def fib(self, n: int) -> int:
        # Base cases: F(0) = 0, F(1) = 1
        if n <= 1:
            return n
        
        # prev2 is F(i-2), prev1 is F(i-1)
        prev2, prev1 = 0, 1
        
        # Calculate from 2 up to n
        for _ in range(2, n + 1):
            current = prev1 + prev2
            # Update pointers for next iteration
            prev2 = prev1
            prev1 = current
            
        return prev1
```

---

## Dry Run (Smart Example)

**Input:** `n = 4`

| Step | Variable `i` | `prev2` | `prev1` | `current` | Explanation |
| :--- | :--- | :--- | :--- | :--- | :--- |
| Init | - | 0 | 1 | - | Initial state for F(0), F(1) |
| 1 | 2 | 1 | 1 | 1 | $0 + 1 = 1$; shift pointers |
| 2 | 3 | 1 | 2 | 2 | $1 + 1 = 2$; shift pointers |
| 3 | 4 | 2 | 3 | 3 | $1 + 2 = 3$; Final Answer |

---

## Edge Cases

- `n = 0`: Should return 0 (Handled by base case).
- `n = 1`: Should return 1 (Handled by base case).
- `n = 2`: Minimum loop execution, returns 1.

---

## Mistakes

- **Exponential Time:** Using naive recursion without memoization in an interview.
- **Off-by-one:** Starting the loop from 1 instead of 2 or incorrect range `(2, n)`.
- **Space Waste:** Using an array `dp = [0] * (n + 1)` when only two variables are needed.
- **User Mistake:** No specific note provided.

---

## Complexity

Time: $O(n)$ → We visit each number from 2 to $n$ exactly once.  
Space: $O(1)$ → Only two variables are used regardless of input size.

---

## Similar Problems

- [Climbing Stairs](https://leetcode.com/problems/climbing-stairs/) - Easy
- [N-th Tribonacci Number](https://leetcode.com/problems/n-th-tribonacci-number/) - Easy
- [House Robber](https://leetcode.com/problems/house-robber/) - Medium

---

## Tags and Properties
  - #dsa #important #revisit #fibonacci #dp
  - [[Dynamic Programming]] [[Space Optimization]]
  - **Revision Date:** 2026-04-10
  - **Problem Link:** [LeetCode - Fibonacci Number](https://leetcode.com/problems/fibonacci-number/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-12)
- [ ] Day 7 Revision (2026-04-17)
- [ ] Day 15 Revision (2026-04-25)
- [ ] Day 30 Revision (2026-05-10)
