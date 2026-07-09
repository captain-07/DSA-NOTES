---
created: 2026-07-10
revisions:
  - 2026-07-12
  - 2026-07-17
  - 2026-07-25
  - 2026-08-09
---

# Generate Parentheses

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Google #Microsoft #Meta #Apple

- **Confidence Checklist:**
  - [ ] Low
  - [ ] Medium
  - [ ] High

- **Concepts:**
  - #backtracking [[Backtracking]], #recursion [[Recursion]], #strings [[Strings]]

## Pattern

Backtracking with Pruning

---
## Difficulty

Medium
#medium

---
## ⚡ Key Idea (Core Insight)

Instead of generating all $2^{2n}$ sequences and validating, build only valid sequences dynamically. We can add a `(` if we have remaining open parentheses, and we can add a `)` only if the count of closed parentheses is less than open parentheses.

---
## ⚡ Quick Recall (VERY IMPORTANT)

Backtrack by passing counts: add `(` if `open < n`, add `)` if `close < open`. Stop when `len(s) == 2 * n`.

---
## Approach

### Brute Force
- Generate all possible $2^{2n}$ combinations of `(` and `)` using recursion. Validate each string.
- Time Complexity: $O(2^{2n} \cdot n)$

### Better
- Not applicable (direct transition from brute force to optimal backtracking is standard).

### Optimal
- Maintain counts of `open` and `close` parentheses.
- Recursively add `(` if `open < n`.
- Recursively add `)` if `close < open`.
- Base case: when the current string length reaches $2 \cdot n$, add it to the results.

---
## Code (Python)

```python
class Solution:
    def generateParenthesis(self, n: int) -> list[str]:
        result = []

        def backtrack(current_str: str, open_count: int, close_count: int):
            # Base case: valid combination found
            if len(current_str) == 2 * n:
                result.append(current_str)
                return

            # Pruning branch 1: add open parenthesis
            if open_count < n:
                backtrack(current_str + "(", open_count + 1, close_count)

            # Pruning branch 2: add close parenthesis
            if close_count < open_count:
                backtrack(current_str + ")", open_count, close_count + 1)

        backtrack("", 0, 0)
        return result
```

---
## Dry Run (Smart Example)

Input: `n = 2`

| Step | Variables | Explanation |
| :--- | :--- | :--- |
| 1 | `s=""`, `open=0`, `close=0` | Start. `open < 2` $\rightarrow$ add `(`. |
| 2 | `s="("`, `open=1`, `close=0` | `open < 2` $\rightarrow$ add `(`. |
| 3 | `s="(("`, `open=2`, `close=0` | `open == 2`. Only `close < open` allows adding `)`. |
| 4 | `s="(()"`, `open=2`, `close=1` | `close < open` $\rightarrow$ add `)`. |
| 5 | `s="(())"`, `open=2`, `close=2` | Length is $2n=4$. Append to result. Backtrack to step 2. |
| 6 | `s="("`, `open=1`, `close=0` | Explore second branch: `close < open` $\rightarrow$ add `)`. |
| 7 | `s="()"`, `open=1`, `close=1` | `open < 2` $\rightarrow$ add `(`. |
| 8 | `s="()("`, `open=2`, `close=1` | `close < open` $\rightarrow$ add `)`. |
| 9 | `s="()()"`, `open=2`, `close=2` | Length is 4. Append to result. |

---
## Edge Cases

- $n = 1$: Output should be `["()"]`.
- $n = 8$: Max constraint; check for recursion limit or potential stack overflow.

---
## Mistakes

- In the brute-force approach, forgetting to check `balance < 0` in the `is_valid` function, which is necessary to ensure a prefix does not contain more closing braces than opening ones.
- Failing to use the pruning and backtracking approach in the optimal version, resulting in generating invalid branches and running into TLE.

---
## Complexity

Time: $O(\frac{4^n}{n\sqrt{n}})$ $\rightarrow$ Bounded by the $n$-th Catalan number, which represents the number of valid parenthesization sequences.
Space: $O(n)$ $\rightarrow$ Maximum depth of the recursion stack is $2n$.

---
## Similar Problems

- [Letter Combinations of a Phone Number](https://leetcode.com/problems/letter-combinations-of-a-phone-number/) - Medium
- [Subsets](https://leetcode.com/problems/subsets/) - Medium
- [Valid Parentheses](https://leetcode.com/problems/valid-parentheses/) - Easy

---
## Tags and Properties

- #dsa #important #revisit #backtracking [[Backtracking]] #strings [[Strings]]
- **Revision Date:** 2026-07-10
- **Problem Link:** [LeetCode - Generate Parentheses](https://leetcode.com/problems/generate-parentheses/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-07-12)
- [ ] Day 7 Revision (2026-07-17)
- [ ] Day 15 Revision (2026-07-25)
- [ ] Day 30 Revision (2026-08-09)
