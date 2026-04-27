---
created: 2026-04-20
revisions:
  - 2026-04-22
  - 2026-04-27
  - 2026-05-05
  - 2026-05-20
---

# Kth Element Of 2 Sorted Arrays

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Google #Microsoft #Flipkart #Apple #Adobe

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #binarysearch [[Binary Search]]
  - #arrays [[Arrays]]
  - #divideandconquer [[Divide and Conquer]]

---
## Pattern

Binary Search on Answer Space / Partitioning

---
## Difficulty

Hard
#hard

---

## ⚡ Key Idea (Core Insight)

The problem is a variation of finding the **Median of Two Sorted Arrays**. Instead of splitting the total length by half, we partition the two arrays such that the **left half contains exactly $k$ elements**. We use Binary Search on the smaller array to find the valid "cut" where `max(Left1) <= min(Right2)` and `max(Left2) <= min(Right1)`.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Binary Search on the **shorter array** to find a partition of size $k$. The range for `low` is `max(0, k-m)` and `high` is `min(k, n)`.

---

## Approach

### Brute Force
- Merge both arrays into a third array, sort it (or use merge step of Merge Sort), and return the $k$-th element.
- **Time:** $O(n + m)$
- **Space:** $O(n + m)$

### Better
- Use two pointers to simulate the merge process. Stop when the counter reaches $k$.
- **Time:** $O(k)$
- **Space:** $O(1)$

### Optimal
- Apply Binary Search on the smaller array (let's say `arr1` of size $n$).
- Partition `arr1` at `mid`. The remaining `k - mid` elements must come from `arr2`.
- Validate the partition: `L1 <= R2` and `L2 <= R1`.
- If `L1 > R2`, we took too many elements from `arr1`, move `high` left.
- If `L2 > R1`, we took too few elements from `arr1`, move `low` right.

---

## Code (Python)

```python
class Solution:
    def kthElement(self, arr1, arr2, n, m, k):
        # Ensure arr1 is the smaller array to optimize binary search range
        if n > m:
            return self.kthElement(arr2, arr1, m, n, k)
        
        # Range of elements we can pick from arr1
        low = max(0, k - m)
        high = min(k, n)
        
        while low <= high:
            cut1 = (low + high) // 2
            cut2 = k - cut1
            
            # Boundary values for L1, R1, L2, R2
            l1 = arr1[cut1 - 1] if cut1 > 0 else float('-inf')
            l2 = arr2[cut2 - 1] if cut2 > 0 else float('-inf')
            r1 = arr1[cut1] if cut1 < n else float('inf')
            r2 = arr2[cut2] if cut2 < m else float('inf')
            
            # Check if partition is valid
            if l1 <= r2 and l2 <= r1:
                return max(l1, l2)
            elif l1 > r2:
                high = cut1 - 1
            else:
                low = cut1 + 1
        
        return -1
```

---

## Dry Run (Smart Example)

**Input:** `arr1 = [2, 3, 6, 7, 9]`, `arr2 = [1, 4, 8, 10]`, `k = 5`

| Step | low | high | cut1 | cut2 | L1, R1 | L2, R2 | Condition | Action |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | 1 | 4 | 2 | 3 | 3, 6 | 8, 10 | 3<=10 & 8<=6? (No) | L2 > R1 -> low=3 |
| 2 | 3 | 4 | 3 | 2 | 6, 7 | 4, 8 | 6<=8 & 4<=7? (Yes) | Return max(6, 4) |
| **Final**| | | | | | | **Result: 6** | |

---

## Edge Cases

- **$k=1$**: Smallest element in both arrays.
- **$k=n+m$**: Largest element in both arrays.
- **$k$ is larger than one array**: `low` must be adjusted to `max(0, k-m)`.
- **Duplicate elements**: Handled correctly by `<=` logic.

---

## Mistakes

- **Incorrect Binary Search Range**: Setting `low=0, high=n` without considering if $k > m$.
- **Not using the smaller array**: BS should always be on the smaller array for $O(\log(\min(n,m)))$.
- **Integer Overflow**: (In C++/Java) when calculating `mid` or comparing large values.
- **User Mistake**: No specific note provided.

---

## Complexity

- **Time:** $O(\log(\min(n, m)))$ → Binary search is performed on the smaller array.
- **Space:** $O(1)$ → Only a few variables used for pointers and partitions.

---

## Similar Problems

- [Median of Two Sorted Arrays](https://leetcode.com/problems/median-of-two-sorted-arrays/) - Hard
- [Find Minimum in Rotated Sorted Array](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/) - Medium
- [Search in Rotated Sorted Array](https://leetcode.com/problems/search-in-rotated-sorted-array/) - Medium

---

## Tags and Properties
- #dsa #important #revisit #binarysearch #coding-interview
- [[Binary Search]] [[Arrays]] [[Partitioning]]
- **Revision Date:** 2026-04-20
- **Problem Link:** [GeeksforGeeks - K-th element of two sorted arrays](https://www.geeksforgeeks.org/problems/k-th-element-of-two-sorted-array1317/1)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-22)
- [ ] Day 7 Revision (2026-04-27)
- [ ] Day 15 Revision (2026-05-05)
- [ ] Day 30 Revision (2026-05-20)
