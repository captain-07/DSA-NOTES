---
created: 2026-04-24
revisions:
  - 2026-04-26
  - 2026-05-01
  - 2026-05-09
  - 2026-05-24
---

# Matrix Median

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Microsoft #Flipkart #Samsung #GoldmanSachs

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #binarysearch [[Binary Search]], #matrix [[Matrix]], #sorting [[Sorting]]

---
## Pattern

Binary Search on Answer Range + Row-wise Binary Search (Counting)

---
## Difficulty

Hard
#hard

---

## ⚡ Key Idea (Core Insight)

The median of a matrix with $N \times M$ elements (where $N \times M$ is odd) is the element which has at least $(N \times M + 1) // 2$ elements less than or equal to it. Since rows are sorted, we can **Binary Search on the value range** $[min, max]$ and use `bisect_right` on each row to count elements $\le mid$ efficiently.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Binary Search for the smallest number $X$ in range $[1, 10^9]$ such that `total_count_less_equal(X) >= (N*M + 1) // 2`.

---

## Approach

### Brute Force
- Flatten the 2D matrix into a 1D array, sort it, and return the middle element.
- Time: $O(NM \log(NM))$
- Space: $O(NM)$

### Optimal
- **Step 1:** Find the search range. `low = min(first column)`, `high = max(last column)`.
- **Step 2:** While `low <= high`, pick `mid`.
- **Step 3:** For each row, calculate how many elements are $\le mid$ using binary search (`bisect_right`).
- **Step 4:** If the total count is less than the required median position $(N \times M + 1) // 2$, move `low = mid + 1`. Otherwise, record `ans = mid` and move `high = mid - 1`.
- Time: $O(32 \cdot N \log M)$ (assuming 32-bit integers)
- Space: $O(1)$

---

## Code (Python)

```python
from bisect import bisect_right

class Solution:
    def findMedian(self, matrix):
        n = len(matrix)
        m = len(matrix[0])
        
        # Range of possible values for binary search
        low = min(row[0] for row in matrix)
        high = max(row[-1] for row in matrix)
        
        required = (n * m + 1) // 2
        ans = low
        
        while low <= high:
            mid = (low + high) // 2
            
            # Count elements <= mid in the whole matrix
            count = 0
            for row in matrix:
                count += bisect_right(row, mid)
            
            if count >= required:
                ans = mid
                high = mid - 1
            else:
                low = mid + 1
                
        return ans
```

---

## Dry Run (Smart Example)

**Input:** `[[1, 3, 5], [2, 6, 9], [3, 6, 9]]`, `N*M=9`, `Required=5th element`

| Step | Low | High | Mid | Total Count ($\le$ Mid) | Explanation |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | 1 | 9 | 5 | `count(1,3,5) + count(2) + count(3) = 3 + 1 + 1 = 5` | Count $\ge 5$, `ans=5`, `high=4` |
| 2 | 1 | 4 | 2 | `count(1) + count(2) + count() = 1 + 1 + 0 = 2` | Count $< 5$, `low=3` |
| 3 | 3 | 4 | 3 | `count(1,3) + count(2) + count(3) = 2 + 1 + 1 = 4` | Count $< 5$, `low=4` |
| 4 | 4 | 4 | 4 | `count(1,3) + count(2) + count(3) = 2 + 1 + 1 = 4` | Count $< 5$, `low=5`. Exit. |

**Result:** 5

---

## Edge Cases

- **Duplicates:** `bisect_right` ensures we find the *smallest* value that satisfies the condition.
- **Single Row/Column:** Algorithm naturally handles $1 \times M$ or $N \times 1$.
- **Negative Values:** Range should be initialized based on matrix min/max, not `0` to `10^9`.

---

## Mistakes

- Using `bisect_left` instead of `bisect_right` (results in incorrect count for duplicates).
- Not initializing `low` and `high` correctly from the matrix boundaries.
- Incorrect median index calculation (for $0$-indexed vs $1$-indexed logic).
- **User Mistake:** No specific note provided.

---

## Complexity

Time: $O(N \cdot \log M \cdot \log(\text{Range}))$ → Range is usually $10^9$, so $\log(\text{Range}) \approx 30-32$.  
Space: $O(1)$ → No extra storage used besides variables.

---

## Similar Problems

- [Kth Smallest Element in a Sorted Matrix](https://leetcode.com/problems/kth-smallest-element-in-a-sorted-matrix/) - Medium
- [Search a 2D Matrix II](https://leetcode.com/problems/search-a-2d-matrix-ii/) - Medium
- [Find K-th Smallest Pair Distance](https://leetcode.com/problems/find-k-th-smallest-pair-distance/) - Hard

---

## Tags and Properties
- #dsa #important #revisit #matrix #binarysearch
- [[Binary Search]] [[Matrix]] [[Kth Smallest]]
- **Problem Link:** [GeeksforGeeks - Matrix Median](https://www.geeksforgeeks.org/problems/matrix-median0728/1)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-26)
- [ ] Day 7 Revision (2026-05-01)
- [ ] Day 15 Revision (2026-05-09)
- [ ] Day 30 Revision (2026-05-24)
