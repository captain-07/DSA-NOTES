---
created: 2026-04-25
revisions:
  - 2026-04-27
  - 2026-05-02
  - 2026-05-10
  - 2026-05-25
---

# Rotate Matrix By 90 Degrees

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Google #Microsoft #Apple #Adobe #Facebook #GoldmanSachs

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #matrix [[Matrix]] #arrays [[Arrays]] #in-place [[In-place]]

## Pattern

Matrix Transpose + Row Reversal  

---
## Difficulty

Medium  
#medium

---

## ⚡ Key Idea (Core Insight)

To rotate an $N \times N$ matrix 90 degrees clockwise in-place:
1.  **Transpose** the matrix (swap $matrix[i][j]$ with $matrix[j][i]$).
2.  **Reverse** each row.
This mapping effectively moves $matrix[i][j]$ to $matrix[j][n-1-i]$.

---

## ⚡ Quick Recall (VERY IMPORTANT)

**Transpose then Reverse** ($M^T \to Reverse$). Swapping symmetric elements across the main diagonal followed by a horizontal flip.

---

## Approach

### Brute Force
- Create a new $N \times N$ matrix and place each element at its rotated position: `new_matrix[j][n-1-i] = matrix[i][j]`.
- **Time:** $O(N^2)$ | **Space:** $O(N^2)$

### Optimal
- **Step 1: Transpose.** Iterate through the upper triangle ($i < j$) and swap $matrix[i][j]$ with $matrix[j][i]$.
- **Step 2: Reverse.** Iterate through each row and reverse the elements using two pointers or built-in reverse.
- **Time:** $O(N^2)$ | **Space:** $O(1)$ (In-place)

---

## Code (Python)

```python
class Solution:
    def rotate(self, matrix: list[list[int]]) -> None:
        """
        Do not return anything, modify matrix in-place instead.
        """
        n = len(matrix)
        
        # 1. Transpose the matrix
        # Swap matrix[i][j] with matrix[j][i]
        for i in range(n):
            for j in range(i + 1, n):
                matrix[i][j], matrix[j][i] = matrix[j][i], matrix[i][j]
        
        # 2. Reverse each row
        for i in range(n):
            matrix[i].reverse()
```

---

## Dry Run (Smart Example)

Input: `[[1, 2, 3], [4, 5, 6], [7, 8, 9]]`

| Step | Variables | Matrix State | Explanation |
| :--- | :--- | :--- | :--- |
| 1 | Initial | `[[1,2,3],[4,5,6],[7,8,9]]` | Input 3x3 matrix |
| 2 | Transpose | `[[1,4,7],[2,5,8],[3,6,9]]` | Swapped (1,2) with (2,1), (1,3) with (3,1), etc. |
| 3 | Reverse R0 | `[[7,4,1],[2,5,8],[3,6,9]]` | Row 0 reversed |
| 4 | Reverse R1 | `[[7,4,1],[8,5,2],[3,6,9]]` | Row 1 reversed |
| 5 | Reverse R2 | `[[7,4,1],[8,5,2],[9,6,3]]` | Row 2 reversed (Final) |

---

## Edge Cases

- **1x1 Matrix:** `[[1]]` remains `[[1]]`.
- **Empty Matrix:** Handled by loop ranges (0 to 0).
- **Already Sorted/Rotated:** The logic still applies and performs the same swaps.
- **Large N:** Complexity remains $O(N^2)$, limited by memory access.

---

## Mistakes

- **Swapping twice during Transpose:** If you loop $j$ from $0$ to $n$, you swap back to the original position. Only loop $j$ from $i+1$ to $n$.
- **Anti-clockwise confusion:** For 90° anti-clockwise, reverse rows *first* then transpose (or transpose then reverse columns).
- **User mistake:** No specific note provided (ensure manual check of transpose boundaries).

---

## Complexity

Time: $O(N^2)$ → We visit every element twice (once for transpose, once for reverse).  
Space: $O(1)$ → All operations are performed in-place without extra data structures.

---

## Similar Problems

- [Rotate Image](https://leetcode.com/problems/rotate-image/) - Medium
- [Determine Whether Matrix Can Be Obtained By Rotation](https://leetcode.com/problems/determine-whether-matrix-can-be-obtained-by-rotation/) - Easy
- [Spiral Matrix](https://leetcode.com/problems/spiral-matrix/) - Medium
- [Set Matrix Zeroes](https://leetcode.com/problems/set-matrix-zeroes/) - Medium

---

## Tags and Properties
  - #dsa #important #revisit #matrix  
  - [[Matrix]] [[In-place]] [[Transpose]]
  - **Revision Date:** 2026-04-25
  - **Problem Link:** [LeetCode - Rotate Image](https://leetcode.com/problems/rotate-image/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-27)
- [ ] Day 7 Revision (2026-05-02)
- [ ] Day 15 Revision (2026-05-10)
- [ ] Day 30 Revision (2026-05-25)
