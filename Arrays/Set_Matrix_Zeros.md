---
created: 2026-04-25
revisions:
  - 2026-04-27
  - 2026-05-02
  - 2026-05-10
  - 2026-05-25
---

# Set Matrix Zeros

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Microsoft #Google #Facebook #Apple #Adobe

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #matrix [[Matrix]]
  - #inplace [[In-place Algorithm]]
  - #arrays [[Arrays]]

## Pattern

Matrix Marker Optimization (In-place storage)

---
## Difficulty

Medium  
#medium

---

## ⚡ Key Idea (Core Insight)

Use the **first row** and **first column** of the matrix itself to store markers for zeros found in the rest of the matrix. Use one additional variable (`col0`) to handle the overlap at `matrix[0][0]`.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Mark zeros in the first row/column. Iterate **backwards** when applying the markers to avoid overwriting the marker logic prematurely.

---

## Approach

### Brute Force
- Create a copy of the matrix. If `original[i][j] == 0`, set row `i` and col `j` to 0 in the copy.
- **Complexity:** Time: O(M * N), Space: O(M * N)

### Better
- Use two auxiliary arrays `row_marker[M]` and `col_marker[N]`. Mark `row_marker[i] = 1` if any element in row `i` is zero.
- **Complexity:** Time: O(M * N), Space: O(M + N)

### Optimal
1.  Initialize a variable `col0 = 1`.
2.  Traverse the matrix. If `matrix[i][j] == 0`:
    - Set `matrix[i][0] = 0`.
    - If `j != 0`, set `matrix[0][j] = 0`. Else, set `col0 = 0`.
3.  Traverse the matrix from `(M-1, N-1)` down to `(0,0)`:
    - If `matrix[i][0] == 0` or `matrix[0][j] == 0` (with `col0` check for column 0), set `matrix[i][j] = 0`.

---

## Code (Python)

```python
class Solution:
    def setZeroes(self, matrix: list[list[int]]) -> None:
        """
        Do not return anything, modify matrix in-place instead.
        """
        m, n = len(matrix), len(matrix[0])
        col0 = 1 # Marker for the first column

        # Step 1: Mark rows and columns using the first row and column
        for i in range(m):
            for j in range(n):
                if matrix[i][j] == 0:
                    matrix[i][0] = 0 # Mark row
                    if j != 0:
                        matrix[0][j] = 0 # Mark column
                    else:
                        col0 = 0 # Special marker for first column

        # Step 2: Set zeros based on markers (iterate backwards)
        for i in range(m - 1, -1, -1):
            for j in range(n - 1, 0, -1):
                if matrix[i][0] == 0 or matrix[0][j] == 0:
                    matrix[i][j] = 0
            if col0 == 0:
                matrix[i][0] = 0
```

---

## Dry Run (Smart Example)

Input: `[[1,1,1],[1,0,1],[1,1,1]]`

| Step | Variables | Explanation |
| :--- | :--- | :--- |
| 1. Marking | `col0=1` | Found `0` at `(1,1)`. Set `matrix[1][0]=0` and `matrix[0][1]=0`. |
| 2. Apply (Bottom-Up) | `i=2, j=2...1` | `matrix[2][0]=1`, `matrix[0][2]=1`, `matrix[0][1]=0`. Row 2 remains same except `matrix[2][1]=0`. |
| 3. Apply (Row 1) | `i=1, j=2...1` | `matrix[1][0]=0` or `matrix[0][j]=0`. Entire Row 1 becomes `[0,0,0]`. |
| 4. Col 0 Check | `col0=1` | `col0` is 1, so `matrix[i][0]` is only zero if its marker was already 0. |

---

## Edge Cases

- **Matrix with no zeros:** Algorithm should leave matrix unchanged.
- **First row/column contains zero:** Handled by `col0` and the marker logic.
- **Single element matrix:** `[0]` becomes `[0]`, `[1]` remains `[1]`.
- **All elements are zero:** Entire matrix correctly becomes zero.

---

## Mistakes

- **Incorrect Overlap Handling:** Forgetting that `matrix[0][0]` is shared by the first row and first column.
- **Forward Iteration:** Updating the matrix while still needing the markers in the first row/column.
- **User mistake:** No specific note provided.

---

## Complexity

Time: O(M * N) → We traverse the matrix twice.  
Space: O(1) → We reuse the first row and column as storage.

---

## Similar Problems

- [Game of Life](https://leetcode.com/problems/game-of-life/) - Medium
- [Valid Sudoku](https://leetcode.com/problems/valid-sudoku/) - Medium
- [Spiral Matrix](https://leetcode.com/problems/spiral-matrix/) - Medium

---

## Tags and Properties
  - #dsa #important #revisit  
  - #matrix [[Matrix]] #inplace [[In-place]]
  - **Revision Date:** 2026-04-25
  - **Problem Link:** [LeetCode - Set Matrix Zeroes](https://leetcode.com/problems/set-matrix-zeroes/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-27)
- [ ] Day 7 Revision (2026-05-02)
- [ ] Day 15 Revision (2026-05-10)
- [ ] Day 30 Revision (2026-05-25)
