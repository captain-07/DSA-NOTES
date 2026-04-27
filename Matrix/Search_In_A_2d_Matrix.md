---
created: 2026-04-22
revisions:
  - 2026-04-24
  - 2026-04-29
  - 2026-05-07
  - 2026-05-22
---

# Search In A 2d Matrix

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Google #Microsoft #Facebook #Apple #Adobe

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #binarysearch [[Binary Search]]
  - #matrix [[Matrix]]
  - #arrays [[Arrays]]

---
## Pattern

Binary Search on Virtual 1D Array

---
## Difficulty

Medium #medium

---

## ⚡ Key Idea (Core Insight)

The matrix is essentially a single sorted list "wrapped" into rows. Because the first element of a row is greater than the last element of the previous row, we can treat the $m \times n$ matrix as a flattened array of length $m \cdot n$ and apply **Standard Binary Search**.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Map 1D index `idx` to 2D coordinates:  
`row = idx // n`  
`col = idx % n`  
(where `n` is the number of columns)

---

## Approach

### Brute Force
- Iterate through every element using nested loops.
- **Time:** $O(m \cdot n)$
- **Space:** $O(1)$

### Better
- Binary search on each row individually.
- **Time:** $O(m \log n)$
- **Space:** $O(1)$

### Optimal
- Use Binary Search on the range $[0, (m \cdot n) - 1]$.
- Calculate the "virtual" 1D index and convert it to 2D to fetch the value.
- Compare with target and adjust `low` or `high` pointers.

---

## Code (Python)

```python
class Solution:
    def searchMatrix(self, matrix: list[list[int]], target: int) -> bool:
        if not matrix or not matrix[0]:
            return False
        
        m, n = len(matrix), len(matrix[0])
        low, high = 0, (m * n) - 1
        
        while low <= high:
            mid = (low + high) // 2
            # Map 1D mid to 2D coordinates
            mid_val = matrix[mid // n][mid % n]
            
            if mid_val == target:
                return True
            elif mid_val < target:
                low = mid + 1
            else:
                high = mid - 1
                
        return False
```

---

## Dry Run (Smart Example)

**Input:** `matrix = [[1, 3, 5], [10, 11, 16], [23, 30, 34]]`, `target = 3`, `m=3, n=3`

| Step | Low | High | Mid | `matrix[mid//n][mid%n]` | Action |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | 0 | 8 | 4 | `matrix[1][1]` = 11 | 11 > 3, `high = 3` |
| 2 | 0 | 3 | 1 | `matrix[0][1]` = 3 | 3 == 3, **Return True** |

---

## Edge Cases

- **Empty Matrix:** `matrix = []` or `matrix = [[]]`.
- **Single Element:** Matrix has only one element (either matches target or doesn't).
- **Target Out of Bounds:** Target is smaller than `matrix[0][0]` or larger than `matrix[m-1][n-1]`.
- **Column Matrix:** Matrix with $m$ rows and only 1 column.

---

## Mistakes

- **Index Mapping:** Using `mid // m` instead of `mid // n` (always divide/mod by the number of **columns**).
- **Boundary Conditions:** Incorrect `high` initialization (should be `m*n - 1`).
- **User Mistake:** No specific note provided.

---

## Complexity

- **Time:** $O(\log(m \cdot n))$ → Standard binary search over $m \cdot n$ elements.
- **Space:** $O(1)$ → Only a few pointers used.

---

## Similar Problems

- [Search a 2D Matrix II](https://leetcode.com/problems/search-a-2d-matrix-ii/) - Medium
- [Find Peak Element II](https://leetcode.com/problems/find-a-peak-element-ii/) - Medium
- [Row with Max 1s](https://www.geeksforgeeks.org/problems/row-with-max-1s0023/1) - Medium

---

## Tags and Properties
- #dsa #important #revisit #matrix #binarysearch
- [[Binary Search]] [[Matrix]]
- **Revision Date:** 2026-04-22
- **Problem Link:** [LeetCode - Search a 2D Matrix](https://leetcode.com/problems/search-a-2d-matrix/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-24)
- [ ] Day 7 Revision (2026-04-29)
- [ ] Day 15 Revision (2026-05-07)
- [ ] Day 30 Revision (2026-05-22)
