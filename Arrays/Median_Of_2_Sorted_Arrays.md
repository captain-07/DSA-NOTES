---
created: 2026-04-20
revisions:
  - 2026-04-22
  - 2026-04-27
  - 2026-05-05
  - 2026-05-20
---

# Median Of 2 Sorted Arrays

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Google #Amazon #Microsoft #Apple #GoldmanSachs #Adobe

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #binarysearch [[Binary Search]]
  - #arrays [[Arrays]]
  - #partitioning [[Partitioning]]

---
## Pattern

Binary Search on Partition Index

---
## Difficulty

Hard  
#hard

---
## ⚡ Key Idea (Core Insight)

Partition both arrays into two halves such that the total number of elements in the left part equals the right part. Use **Binary Search on the smaller array** to find a split point where `max(Left1) <= min(Right2)` and `max(Left2) <= min(Right1)`.

---
## ⚡ Quick Recall (VERY IMPORTANT)

Binary search the split point in the **shorter array**. Ensure cross-boundary elements are valid: `L1 <= R2` and `L2 <= R1`. Median is either `max(L1, L2)` (odd) or `avg(max(L1, L2), min(R1, R2))` (even).

---
## Approach

### Brute Force
- Merge both arrays into a single sorted array, then return the middle element.
- **Time:** $O(M + N)$
- **Space:** $O(M + N)$

### Better
- Use a two-pointer approach to iterate until the $(M+N)/2$-th element without creating a new array.
- **Time:** $O(M + N)$
- **Space:** $O(1)$

### Optimal
- Perform Binary Search on the partition index of the smaller array.
- For a partition `i` in `A` and `j` in `B`, ensure `i + j = (total_len + 1) // 2`.
- Handle boundary conditions using $-\infty$ and $+\infty$.
- **Time:** $O(\log(\min(M, N)))$
- **Space:** $O(1)$

---
## Code (Python)

```python
class Solution:
    def findMedianSortedArrays(self, nums1: list[int], nums2: list[int]) -> float:
        # Ensure nums1 is the smaller array to optimize Binary Search
        if len(nums1) > len(nums2):
            nums1, nums2 = nums2, nums1
            
        m, n = len(nums1), len(nums2)
        low, high = 0, m
        total_half = (m + n + 1) // 2
        
        while low <= high:
            partition1 = (low + high) // 2
            partition2 = total_half - partition1
            
            # Boundary values
            maxLeft1 = nums1[partition1 - 1] if partition1 > 0 else float('-inf')
            minRight1 = nums1[partition1] if partition1 < m else float('inf')
            
            maxLeft2 = nums2[partition2 - 1] if partition2 > 0 else float('-inf')
            minRight2 = nums2[partition2] if partition2 < n else float('inf')
            
            if maxLeft1 <= minRight2 and maxLeft2 <= minRight1:
                # Correct partition found
                if (m + n) % 2 == 1:
                    return float(max(maxLeft1, maxLeft2))
                else:
                    return (max(maxLeft1, maxLeft2) + min(minRight1, minRight2)) / 2.0
            elif maxLeft1 > minRight2:
                high = partition1 - 1
            else:
                low = partition1 + 1
        return 0.0
```

---
## Dry Run (Smart Example)

**Input:** `nums1 = [1, 3]`, `nums2 = [2]`  
**Total Length:** 3 (Odd) | **total_half:** 2

| Step | low, high | part1, part2 | Left/Right Vals | Comparison | Result |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | 0, 2 | 1, 1 | L1=1, R1=3; L2=2, R2=inf | 1 <= inf (T), 2 <= 3 (T) | Found |
| 2 | - | - | max(1, 2) = 2 | - | 2.0 |

---
## Edge Cases

- **One array is empty:** Binary search handles via `low/high` on size 0, or code falls back to logic correctly.
- **Arrays of size 1:** Standard partition logic applies.
- **All elements in A < all elements in B:** `partition1` will reach `m` or `0`.
- **Negative numbers:** Handled correctly by standard comparisons.

---
## Mistakes

- Not ensuring `nums1` is the shorter array (causes index out of bounds on `partition2`).
- Incorrect calculation of `total_half` for odd/even parity.
- Forgetting to handle empty array boundaries with `inf`/-`inf`.
- **User Mistake:** No specific note provided.

---
## Complexity

Time: $O(\log(\min(M, N)))$ → Binary search is only performed on the smaller array.  
Space: $O(1)$ → Only a few pointers/variables used.

---
## Similar Problems

- [Kth Element of Two Sorted Arrays](https://www.geeksforgeeks.org/k-th-element-two-sorted-arrays/) - Medium
- [Median of a Row Wise Sorted Matrix](https://www.interviewbit.com/problems/matrix-median/) - Hard
- [Search in Rotated Sorted Array](https://leetcode.com/problems/search-in-rotated-sorted-array/) - Medium

---
## Tags and Properties
  - #dsa #important #revisit  
  - #hard #binarysearch #partitioning
  - [[Binary Search]] [[Arrays]]
  - **Revision Date:** 2026-04-20
  - **Problem Link:** [LeetCode - Median of Two Sorted Arrays](https://leetcode.com/problems/median-of-two-sorted-arrays/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-22)
- [ ] Day 7 Revision (2026-04-27)
- [ ] Day 15 Revision (2026-05-05)
- [ ] Day 30 Revision (2026-05-20)
