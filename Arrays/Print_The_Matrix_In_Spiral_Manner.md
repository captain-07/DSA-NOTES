---
created: 2026-04-25
revisions:
  - 2026-04-27
  - 2026-05-02
  - 2026-05-10
  - 2026-05-25
---

# Print The Matrix In Spiral Manner

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Microsoft #Google #Apple #Adobe #Uber

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #arrays [[Arrays]]
  - #matrix [[Matrix]]
  - #simulation [[Simulation]]

---
## Pattern

Boundary Shrinking (Four Pointers)

---
## Difficulty

Medium  
#medium

---

## ⚡ Key Idea (Core Insight)

Maintain four boundaries (`top`, `bottom`, `left`, `right`). Iterate in a cycle (Right → Down → Left → Up), updating the corresponding boundary after each traversal to "shrink" the search space until boundaries cross.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Four pointers + 4 `while/for` loops. **Crucial:** After the first two movements (Right and Down), check if `top <= bottom` and `left <= right` again before moving Left and Up to avoid duplicate processing in non-square matrices.

---

## Approach

### Brute Force
- Standard simulation is already the most efficient way to visit every element.
- Time: O(M × N) | Space: O(1) (excluding output)

### Better
- N/A (Simulation is the standard optimal approach).

### Optimal
1. Initialize `top = 0`, `left = 0`, `bottom = rows - 1`, `right = cols - 1`.
2. While `top <= bottom` and `left <= right`:
   - Traverse `left` to `right` along `top` row, then `top += 1`.
   - Traverse `top` to `bottom` along `right` column, then `right -= 1`.
   - **Check** `top <= bottom`, then traverse `right` to `left` along `bottom` row, then `bottom -= 1`.
   - **Check** `left <= right`, then traverse `bottom` to `top` along `left` column, then `left += 1`.

---

## Code (Python)

```python
class Solution:
    def spiralOrder(self, matrix: list[list[int]]) -> list[int]:
        if not matrix or not matrix[0]:
            return []
        
        res = []
        top, bottom = 0, len(matrix) - 1
        left, right = 0, len(matrix[0]) - 1
        
        while top <= bottom and left <= right:
            # 1. Right: Traverse top row
            for i in range(left, right + 1):
                res.append(matrix[top][i])
            top += 1
            
            # 2. Down: Traverse right column
            for i in range(top, bottom + 1):
                res.append(matrix[i][right])
            right -= 1
            
            # 3. Left: Traverse bottom row (Check if row still exists)
            if top <= bottom:
                for i in range(right, left - 1, -1):
                    res.append(matrix[bottom][i])
                bottom -= 1
                
            # 4. Up: Traverse left column (Check if column still exists)
            if left <= right:
                for i in range(bottom, top - 1, -1):
                    res.append(matrix[i][left])
                left += 1
                
        return res
```

---

## Dry Run (Smart Example)

Input: `matrix = [[1,2,3],[4,5,6],[7,8,9]]`

| Step | Variables (T, B, L, R) | Action | Explanation |
| :--- | :--- | :--- | :--- |
| 1 | 0, 2, 0, 2 | Right (T=0, L to R) | `res = [1,2,3]`, `top` becomes 1 |
| 2 | 1, 2, 0, 2 | Down (R=2, T to B) | `res = [1,2,3,6,9]`, `right` becomes 1 |
| 3 | 1, 2, 0, 1 | Left (B=2, R to L) | `res = [1,2,3,6,9,8,7]`, `bottom` becomes 1 |
| 4 | 1, 1, 0, 1 | Up (L=0, B to T) | `res = [1,2,3,6,9,8,7,4]`, `left` becomes 1 |
| 5 | 1, 1, 1, 1 | Right (T=1, L to R) | `res = [1,2,3,6,9,8,7,4,5]`, `top` becomes 2. Loop breaks. |

---

## Edge Cases

- **Empty Matrix:** Return `[]` immediately.
- **Single Row:** Loop 1 completes, `top > bottom` prevents others.
- **Single Column:** Loop 1 and 2 complete, `left > right` prevents others.
- **Rectangular Matrix:** Boundary checks inside the loop prevent duplicate elements.

---

## Mistakes

- **Inner Checks:** Forgetting to check `top <= bottom` before moving Left and `left <= right` before moving Up.
- **Off-by-one:** Incorrect range boundaries in `range(right, left - 1, -1)`.
- **User Mistake:** No specific note provided.

---

## Complexity

Time: O(M × N) → Every element is visited exactly once.  
Space: O(1) → Constant extra space used for pointers (ignoring output array).

---

## Similar Problems

- [Spiral Matrix II](https://leetcode.com/problems/spiral-matrix-ii/) - Medium
- [Spiral Matrix III](https://leetcode.com/problems/spiral-matrix-iii/) - Medium
- [Rotate Image](https://leetcode.com/problems/rotate-image/) - Medium
- [Diagonal Traverse](https://leetcode.com/problems/diagonal-traverse/) - Medium

---

## Tags and Properties
  - #dsa #important #revisit  
  - #matrix #simulation #arrays
  - [[Matrix]] [[Arrays]]
  - **Revision Date:** 2026-04-25
  - **Problem Link:** [LeetCode - Spiral Matrix](https://leetcode.com/problems/spiral-matrix/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-27)
- [ ] Day 7 Revision (2026-05-02)
- [ ] Day 15 Revision (2026-05-10)
- [ ] Day 30 Revision (2026-05-25)
