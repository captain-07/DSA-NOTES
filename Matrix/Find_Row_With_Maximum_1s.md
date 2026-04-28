---
created: 2026-04-22
revisions:
  - 2026-04-24
  - 2026-04-29
  - 2026-05-07
  - 2026-05-22
---

# Find Row With Maximum 1s

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Microsoft #Samsung #Media.net #Adobe

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #matrix [[Matrix]]
  - #binarysearch [[Binary Search]]
  - #pointers [[Two Pointers]]

## Pattern

Staircase Search (Top-Right to Bottom-Left)  
Binary Search on Sorted Rows

---
## Difficulty

Medium  
#medium

---

## ⚡ Key Idea (Core Insight)

Each row is **sorted**. A row has more 1s if its first '1' appears earlier (further left) than the current best row. Instead of counting every row, we only move left when we find a 1 and down when we hit a 0.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Start at `(0, m-1)`. If `1`, move **Left** (update `max_row`); if `0`, move **Down**.

---

## Approach

### Brute Force
- Iterate through every element of the matrix and count 1s for each row. Keep track of the maximum count.
- **Time:** $O(N \times M)$

### Better
- Since rows are sorted, use **Binary Search** to find the first occurrence of `1` in each row.
- `Count = Total Columns - Index of first 1`.
- **Time:** $O(N \log M)$

### Optimal (Staircase)
- Start at the top-right corner $(i=0, j=M-1)$.
- If `matrix[i][j] == 1`, move left to see if there are more 1s in the same row and update the answer.
- If `matrix[i][j] == 0`, move down because no more 1s can exist to the left in this row.
- **Time:** $O(N + M)$

---

## Code (Python)

```python
class Solution:
    def rowWithMax1s(self, arr: list[list[int]]) -> int:
        if not arr:
            return -1
            
        n = len(arr)
        m = len(arr[0])
        
        max_row_idx = -1
        # Start from the top-right corner
        j = m - 1 
        
        for i in range(n):
            # Move left while you encounter 1s
            found_one = False
            while j >= 0 and arr[i][j] == 1:
                j -= 1
                max_row_idx = i
                found_one = True
            
            # Note: We don't reset 'j' because we only care 
            # about rows that have 1s further left than current 'j'
        
        return max_row_idx
```

---

## Dry Run (Smart Example)

**Input:** `[[0, 1, 1], [1, 1, 1], [0, 0, 0]]` ($N=3, M=3$)

| Step | (i, j) | arr[i][j] | Action | max_row_idx |
| :--- | :--- | :--- | :--- | :--- |
| 1 | (0, 2) | 1 | Move Left (j=1) | 0 |
| 2 | (0, 1) | 1 | Move Left (j=0) | 0 |
| 3 | (0, 0) | 0 | Move Down (i=1) | 0 |
| 4 | (1, 0) | 1 | Move Left (j=-1) | 1 |
| 5 | (2, -1)| - | j < 0, Exit Row Loop | 1 |

---

## Edge Cases

- **All 0s:** Should return -1.
- **All 1s:** Should return 0 (first row).
- **Empty Matrix:** Handle `len(arr) == 0`.
- **Single Row/Column:** Logic holds; staircase simply terminates faster.

---

## Mistakes

- Resetting the column pointer `j` to `M-1` for every row (this makes it $O(N \times M)$).
- Not returning `-1` when no 1s are found.
- **User Mistake:** No specific note provided.

---

## Complexity

Time: $O(N + M)$ → We traverse at most $N$ rows and $M$ columns.  
Space: $O(1)$ → No extra data structures used.

---

## Similar Problems

- [Search a 2D Matrix II](https://leetcode.com/problems/search-a-2d-matrix-ii/) - Medium
- [Count 1s in a Sorted Binary Array](https://www.geeksforgeeks.org/count-1s-sorted-binary-array/) - Easy
- [Search in a Sorted Matrix](https://leetcode.com/problems/search-a-2d-matrix/) - Medium

---

## Tags and Properties
- #dsa #important #revisit #matrix
- [[Matrix]] [[Binary Search]] [[Pointers]]
- **Problem Link:** [GeeksforGeeks - Row with max 1s](https://www.geeksforgeeks.org/problems/row-with-max-1s0023/1)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-24)
- [ ] Day 7 Revision (2026-04-29)
- [ ] Day 15 Revision (2026-05-07)
- [ ] Day 30 Revision (2026-05-22)
