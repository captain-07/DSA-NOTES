---
created: 2026-04-22
revisions:
  - 2026-04-24
  - 2026-04-29
  - 2026-05-07
  - 2026-05-22
---

# Search In A 2d Matrix-II

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Microsoft #Google #Apple #Oracle #Adobe

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #matrix [[Matrix]]
  - #binarysearch [[Binary Search]]
  - #twopointers [[Two Pointers]]

## Pattern

Search Space Reduction (Staircase Search)

---
## Difficulty

Medium  
#medium

---

## ⚡ Key Idea (Core Insight)

The matrix is sorted both row-wise and column-wise. By starting at the **Top-Right** (or Bottom-Left) corner, each comparison allows you to eliminate an entire row or column. It effectively treats the corner as a decision node: moving left decreases the value, moving down increases it.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Start at `(0, last_col)`. If target is smaller, move **Left**; if larger, move **Down**.

---

## Approach

### Brute Force
- Iterate through every element $M \times N$ using nested loops.
- Time: $O(M \times N)$

### Better
- Perform Binary Search on each of the $M$ rows.
- Time: $O(M \log N)$

### Optimal
- **Staircase Search:** Start at top-right corner `(r=0, c=cols-1)`.
- If `matrix[r][c] == target`, return True.
- If `matrix[r][c] > target`, the entire column must be greater than target $\rightarrow$ `c -= 1`.
- If `matrix[r][c] < target`, the entire row must be smaller than target $\rightarrow$ `r += 1`.
- Continue until out of bounds.

---

## Code (Python)

```python
class Solution:
    def searchMatrix(self, matrix: list[list[int]], target: int) -> bool:
        if not matrix or not matrix[0]:
            return False
            
        rows, cols = len(matrix), len(matrix[0])
        # Start at Top-Right corner
        r, c = 0, cols - 1
        
        while r < rows and c >= 0:
            current = matrix[r][c]
            
            if current == target:
                return True
            elif current > target:
                # Eliminate current column
                c -= 1
            else:
                # Eliminate current row
                r += 1
                
        return False
```

---

## Dry Run (Smart Example)

**Input:** `matrix = [[1, 4, 7], [2, 5, 8], [3, 6, 9]]`, `target = 6`

| Step | (r, c) | Value | Explanation |
| :--- | :--- | :--- | :--- |
| 1 | (0, 2) | 7 | $7 > 6 \rightarrow$ Move Left (c=1) |
| 2 | (0, 1) | 4 | $4 < 6 \rightarrow$ Move Down (r=1) |
| 3 | (1, 1) | 5 | $5 < 6 \rightarrow$ Move Down (r=2) |
| 4 | (2, 1) | 6 | **Match!** Return True |

---

## Edge Cases

- **Empty Matrix:** Handle `if not matrix` to avoid index errors.
- **Target < Minimum:** Start comparison at top-right will immediately move left until out of bounds.
- **Target > Maximum:** Start comparison will move down until out of bounds.
- **Single Element Matrix:** Correctly handles `while` loop condition.

---

## Mistakes

- **Starting at (0,0):** Both right and down increase values, providing no way to eliminate search space.
- **Confusion with Matrix I:** In Matrix I, the first element of a row is greater than the last of the previous; here, they are independent but sorted.
- **Off-by-one:** Ensure `c >= 0` and `r < rows` boundaries are strict.
- **User Mistake:** No specific note provided.

---

## Complexity

Time: O(M + N) → In the worst case, you traverse from the top-right to the bottom-left corner.  
Space: O(1) → Only pointer variables are used.

---

## Similar Problems

- [Search a 2D Matrix](https://leetcode.com/problems/search-a-2d-matrix/) - Medium
- [Kth Smallest Element in a Sorted Matrix](https://leetcode.com/problems/kth-smallest-element-in-a-sorted-matrix/) - Medium
- [Count Negative Numbers in a Sorted Matrix](https://leetcode.com/problems/count-negative-numbers-in-a-sorted-matrix/) - Easy

---

## Tags and Properties
  - #dsa #important #revisit  
  - #matrix [[Matrix]] #searchspace [[Search Space Reduction]]
  - Revision Date: 2026-04-22
  - **Problem Link:** [LeetCode - Search a 2D Matrix II](https://leetcode.com/problems/search-a-2d-matrix-ii/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-24)
- [ ] Day 7 Revision (2026-04-29)
- [ ] Day 15 Revision (2026-05-07)
- [ ] Day 30 Revision (2026-05-22)
