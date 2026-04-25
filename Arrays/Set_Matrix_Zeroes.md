---
created: 2026-04-25
revisions:
  - 2026-04-27
  - 2026-05-02
  - 2026-05-10
  - 2026-05-25
---

# Set Matrix Zeroes

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Microsoft #Google #Facebook #Apple #Adobe

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #arrays [[Arrays]], #matrix [[Matrix]], #space-optimization [[Space Optimization]]

## Pattern

In-place State Tracking  
Using First Row/Column as Marker

---
## Difficulty

Medium  
#medium

---

## ⚡ Key Idea (Core Insight)

The bottleneck is tracking which rows/cols to zero without affecting future checks. Instead of using extra arrays, use the **first row** and **first column** of the matrix itself as your markers. Use a single auxiliary variable to handle the overlap at `matrix[0][0]`.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Mark `matrix[0][j]` and `matrix[i][0]` as 0 when `matrix[i][j] == 0`. Iterate **backwards** during the update phase to avoid corrupting the markers.

---

## Approach

### Brute Force
- Iterate through the matrix. If an element is 0, mark its entire row and column with a dummy value (e.g., -99999) that doesn't exist in the input. Finally, replace all dummies with 0.
- **Time:** O(N*M * (N+M))
- **Space:** O(1) if dummy values are possible, else O(N*M)

### Better
- Use two separate boolean arrays: `row[M]` and `col[N]`. Traverse matrix, if `matrix[i][j] == 0`, set `row[i] = True` and `col[j] = True`. Update matrix in a second pass.
- **Time:** O(N*M)
- **Space:** O(N + M)

### Optimal
- Use `matrix[0][..]` and `matrix[..][0]` as the marker arrays.
- Since `matrix[0][0]` is shared, use a variable `col0` to track the first column's state.
- 1. Traverse matrix: If `matrix[i][j] == 0`, mark `matrix[i][0] = 0` and `matrix[0][j] = 0`.
- 2. Traverse matrix **backwards** (from bottom-right to (0,0)): If marker is 0, set element to 0.
- **Time:** O(N*M)
- **Space:** O(1)

---

## Code (Python)

```python
class Solution:
    def setZeroes(self, matrix: list[list[int]]) -> None:
        """
        Do not return anything, modify matrix in-place instead.
        """
        rows = len(matrix)
        cols = len(matrix[0])
        col0 = 1 # Flag for the first column

        # Step 1: Mark rows and columns using the first row/col
        for i in range(rows):
            if matrix[i][0] == 0:
                col0 = 0
            for j in range(1, cols):
                if matrix[i][j] == 0:
                    matrix[i][0] = 0
                    matrix[0][j] = 0

        # Step 2: Iterate backwards to populate zeros
        for i in range(rows - 1, -1, -1):
            for j in range(cols - 1, 0, -1):
                if matrix[i][0] == 0 or matrix[0][j] == 0:
                    matrix[i][j] = 0
            if col0 == 0:
                matrix[i][0] = 0
```

---

## Dry Run (Smart Example)

Input: `[[0, 1, 2, 0], [3, 4, 5, 2], [1, 3, 1, 5]]`

| Step | Variables | Explanation |
| :--- | :--- | :--- |
| 1. Marking | `i=0, j=0` | `matrix[0][0]` is 0, so `col0 = 0`. |
| 2. Marking | `i=0, j=3` | `matrix[0][3]` is 0, so `matrix[0][3]=0` and `matrix[0][0]=0`. |
| 3. Update (Back) | `i=2, j=3` | `matrix[0][3]` is 0, so `matrix[2][3]` becomes 0. |
| 4. Update (Back) | `i=1, j=1` | Markers `matrix[1][0]=3`, `matrix[0][1]=1`. No change. |
| 5. Final Row | `i=0, col0=0` | `col0` is 0, so `matrix[0][0]` becomes 0. |

---

## Edge Cases

- **Matrix with no zeros:** Algorithm should leave matrix unchanged.
- **First row/column only zeros:** Handled by `col0` and the backward pass.
- **Single element matrix:** Works correctly with the logic.
- **All elements are zero:** Correctly zeros the entire matrix.

---

## Mistakes

- Updating the matrix while still scanning for zeros (results in all zeros).
- Incorrectly handling the overlap at `matrix[0][0]`.
- Forgetting to process the first row/column state last or in a specific direction.
- **User Mistake:** No specific note provided.

---

## Complexity

- **Time:** O(M * N) → Two full passes of the matrix.
- **Space:** O(1) → Constant extra space used (`col0` variable).

---

## Similar Problems

- [Game of Life](https://leetcode.com/problems/game-of-life/) - Medium
- [Spiral Matrix](https://leetcode.com/problems/spiral-matrix/) - Medium
- [Rotate Image](https://leetcode.com/problems/rotate-image/) - Medium

---

## Tags and Properties
- #dsa #important #revisit #matrix #in-place
- [[Matrix]] [[Space Optimization]]
- **Revision Date:** 2026-04-25
- **Problem Link:** [LeetCode - Set Matrix Zeroes](https://leetcode.com/problems/set-matrix-zeroes/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-27)
- [ ] Day 7 Revision (2026-05-02)
- [ ] Day 15 Revision (2026-05-10)
- [ ] Day 30 Revision (2026-05-25)
