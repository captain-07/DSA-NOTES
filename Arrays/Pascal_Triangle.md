---
created: 2026-04-25
revisions:
  - 2026-04-27
  - 2026-05-02
  - 2026-05-10
  - 2026-05-25
---

# Pascal Triangle

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Microsoft #Google #GoldmanSachs #Adobe

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #arrays [[Arrays]]
  - #dynamicprogramming [[Dynamic Programming]]
  - #math [[Mathematics]]

---
## Pattern

Simulation (Row-by-Row Generation)  
Dynamic Programming (Tabulation)

---
## Difficulty

Easy  
#easy

---

## ⚡ Key Idea (Core Insight)

The triangle is built row-by-row. Every row starts and ends with **1**. Every interior element at `row[i][j]` is simply the sum of the two elements directly above it: `row[i-1][j-1] + row[i-1][j]`.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Nested loops: Outer loop for row index $i$, inner loop for element index $j$.  
`current_row[j] = prev_row[j-1] + prev_row[j]`

---

## Approach

### Brute Force
- Calculate each element using the combination formula $nCr = \frac{n!}{r!(n-r)!}$ independently.
- Time: $O(N^3)$ due to factorial calculations for each of the $N^2$ elements.

### Better
- Use the previous row to compute the current row. 
- Avoids redundant factorials by using the additive property.
- Time: $O(N^2)$

### Optimal
- **Full Triangle:** Iteratively build each row. Append `1`, calculate middle elements using the previous row's sliding window of 2, and append `1`.
- **Specific Row $K$ (Optimization):** If only row $K$ is needed, use the property: $element_j = element_{j-1} \times \frac{row - (j-1)}{j}$. This allows $O(N)$ time and $O(1)$ extra space.

---

## Code (Python)

```python
class Solution:
    def generate(self, numRows: int) -> list[list[int]]:
        # Initialize result with the first row
        triangle = [[1]]
        
        for i in range(1, numRows):
            prev_row = triangle[-1]
            # Every row starts with 1
            curr_row = [1]
            
            # Calculate interior elements
            for j in range(1, i):
                curr_row.append(prev_row[j-1] + prev_row[j])
            
            # Every row ends with 1
            curr_row.append(1)
            triangle.append(curr_row)
            
        return triangle
```

---

## Dry Run (Smart Example)

Input: `numRows = 4`

| Step | Row Index (i) | Previous Row | Current Row Calculation | Resulting Row |
| :--- | :--- | :--- | :--- | :--- |
| 1 | 0 | None | Initial state | `[1]` |
| 2 | 1 | `[1]` | Start: `[1]`, End: `1` | `[1, 1]` |
| 3 | 2 | `[1, 1]` | `[1]` + `(1+1)` + `[1]` | `[1, 2, 1]` |
| 4 | 3 | `[1, 2, 1]` | `[1]` + `(1+2), (2+1)` + `[1]` | `[1, 3, 3, 1]` |

---

## Edge Cases

- `numRows = 1`: Should return `[[1]]` immediately.
- `numRows = 0`: Depending on constraints, returns `[]`.
- Large `numRows`: Standard $O(N^2)$ logic holds; check for integer overflow in other languages (not Python).

---

## Mistakes

- **Index Out of Bounds:** Trying to access `prev_row[j]` when $j$ is the last index.
- **Initialization:** Forgetting to handle the first row `[[1]]` as the base case.
- **User Mistake:** No specific note provided (Ensure to document the $nCr$ property for specific row queries).

---

## Complexity

Time: $O(N^2)$ → We calculate each of the $\frac{N(N+1)}{2}$ elements exactly once.  
Space: $O(N^2)$ → To store the generated triangle rows.

---

## Similar Problems

- [Pascal's Triangle II](https://leetcode.com/problems/pascals-triangle-ii/) - Easy
- [Fibonacci Number](https://leetcode.com/problems/fibonacci-number/) - Easy
- [Combinations](https://leetcode.com/problems/combinations/) - Medium

---

## Tags and Properties
- #dsa #important #revisit #simulation #math
- [[Arrays]] [[Dynamic Programming]]
- **Revision Date:** 2026-04-25
- **Problem Link:** [LeetCode - Pascal's Triangle](https://leetcode.com/problems/pascals-triangle/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-27)
- [ ] Day 7 Revision (2026-05-02)
- [ ] Day 15 Revision (2026-05-10)
- [ ] Day 30 Revision (2026-05-25)
