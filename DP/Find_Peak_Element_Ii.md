---
created: 2026-04-24
revisions:
  - 2026-04-26
  - 2026-05-01
  - 2026-05-09
  - 2026-05-24
---

# Find Peak Element-Ii

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Google #Amazon #Microsoft #Uber #Directi

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #binarysearch [[Binary Search]]
  - #matrix [[Matrix]]
  - #divideandconquer [[Divide and Conquer]]

---
## Pattern

Binary Search on 2D Search Space (Dimension Reduction)

---
## Difficulty

Hard  
#hard

---

## ⚡ Key Idea (Core Insight)

To find a peak in 2D, **Binary Search on columns**. For a `midCol`, find the row index of the **global maximum** in that column. Since it's the max in its column, it's already greater than its top/bottom neighbors. You only need to compare it with its left and right neighbors to decide which half of the matrix to discard.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Binary search `low/high` on columns. At `mid`, find `maxRow`. If `mat[maxRow][mid]` < `mat[maxRow][mid+1]`, peak is to the right; else left.

---

## Approach

### Brute Force
- Iterate through every element in the $M \times N$ matrix and check all 4 neighbors.
- **Time:** $O(M \times N)$

### Optimal
1. Perform binary search on column indices ($0$ to $n-1$).
2. For `midCol`, find the row index `maxRow` such that `mat[maxRow][midCol]` is the maximum in that column.
3. Compare `mat[maxRow][midCol]` with its horizontal neighbors:
   - If `mat[maxRow][midCol] < mat[maxRow][midCol + 1]`: The peak must exist in the right half ($low = midCol + 1$).
   - Else: The peak exists in the left half or is the current element ($high = midCol$).
4. Return the coordinates once $low == high$.
- **Time:** $O(M \log N)$

---

## Code (Python)

```python
class Solution:
    def findPeakGrid(self, mat: list[list[int]]) -> list[int]:
        rows = len(mat)
        cols = len(mat[0])
        low = 0
        high = cols - 1
        
        while low <= high:
            mid_col = (low + high) // 2
            
            # Find the max element's row in the current mid_col
            max_row = 0
            for r in range(rows):
                if mat[r][mid_col] > mat[max_row][mid_col]:
                    max_row = r
            
            # Check left and right neighbors
            left_is_greater = mid_col > low and mat[max_row][mid_col - 1] > mat[max_row][mid_col]
            right_is_greater = mid_col < high and mat[max_row][mid_col + 1] > mat[max_row][mid_col]
            
            if not left_is_greater and not right_is_greater:
                return [max_row, mid_col]
            elif right_is_greater:
                low = mid_col + 1
            else:
                high = mid_col - 1
                
        return []
```

---

## Dry Run (Smart Example)

Input: `[[10, 20, 15], [21, 30, 14], [7, 16, 32]]`

| Step | low/high | midCol | maxRow (in midCol) | Comparison | Action |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | 0, 2 | 1 | 1 (val: 30) | 30 > 20(L), 30 > 14(R) | **Peak Found!** |
| 2 | - | - | - | (If 30 was < 14) | Move low to 2 |

---

## Edge Cases

- **Single Column/Row:** Binary search still works; `maxRow` logic covers single column.
- **Strictly Increasing/Decreasing rows:** Peak will be at the boundaries.
- **Peak at corners:** Handled by boundary checks in neighbor comparison.

---

## Mistakes

- **Checking all 4 neighbors for every element:** Too slow ($O(N \times M)$).
- **Binary searching 1D peak on every row:** Only gives a row-peak, not necessarily a grid-peak.
- **User mistake:** No specific note provided.

---

## Complexity

- **Time:** $O(M \log N)$ → $O(\log N)$ steps for binary search, $O(M)$ to find max in column.
- **Space:** $O(1)$ → No extra data structures used.

---

## Similar Problems

- [Find Peak Element](https://leetcode.com/problems/find-peak-element/) - Medium
- [Search a 2D Matrix II](https://leetcode.com/problems/search-a-2d-matrix-ii/) - Medium
- [Find Kth Smallest Pair Distance](https://leetcode.com/problems/find-k-th-smallest-pair-distance/) - Hard

---

## Tags and Properties
- #dsa #important #revisit #binarysearch #matrix
- [[Binary Search]] [[Matrix]]
- **Revision Date:** 2026-04-24
- **Problem Link:** [LeetCode - Find Peak Element II](https://leetcode.com/problems/find-a-peak-element-ii/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-26)
- [ ] Day 7 Revision (2026-05-01)
- [ ] Day 15 Revision (2026-05-09)
- [ ] Day 30 Revision (2026-05-24)
