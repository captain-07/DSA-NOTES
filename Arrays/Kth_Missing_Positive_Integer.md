---
created: 2026-04-11
revisions:
  - 2026-04-13
  - 2026-04-18
  - 2026-04-26
  - 2026-05-11
---

Here is the comprehensive, structured DSA note for Obsidian.

---

# 📔 Kth Missing Positive Integer

> [!abstract] **Properties**
> **Pattern:** #BinarySearch 
> **Difficulty:** 🟢 Easy / 🟡 Medium
> **LeetCode:** [1539. Kth Missing Positive Integer](https://leetcode.com/problems/kth-missing-positive-integer/)

---

## 🧩 Key Idea
The core insight is that for any index `i`, the count of missing numbers before `arr[i]` is exactly **`arr[i] - (i + 1)`**, because in a perfectly sequential array (e.g., `[1, 2, 3...]`), the value at `i` should be `i + 1`.

---

## 🚀 Approach

The **Optimal Approach** leverages the sorted property of the array to perform a **Binary Search** in $O(\log N)$ time, rather than a linear scan.

1. **Calculate Missing Count:** At any midpoint `mid`, calculate how many numbers are missing before that element:
   `missing_count = arr[mid] - (mid + 1)`
2. **Binary Search Logic:**
   - If `missing_count < k`: We haven't reached the $k^{th}$ missing number yet. Search the **right** half (`low = mid + 1`).
   - If `missing_count >= k`: The $k^{th}$ missing number is at or before this index. Search the **left** half (`high = mid - 1`).
3. **The Result Formula:**
   After the search, the `low` pointer will be at the index where the $k^{th}$ missing number "should" have been. The final answer is simply **`low + k`**.

---

## 💻 Code

```java
class Solution {
    public int findKthPositive(int[] arr, int k) {
        int low = 0, high = arr.length - 1;

        // Binary search to find the range where the kth missing number lies
        while (low <= high) {
            int mid = low + (high - low) / 2;
            int missing = arr[mid] - (mid + 1);

            if (missing < k) {
                low = mid + 1;
            } else {
                high = mid - 1;
            }
        }

        // Final formula: k + (high + 1) which simplifies to low + k
        return low + k;
    }
}
```

---

## 🏗️ Pattern
**Binary Search on Search Space / Index Property:** This problem uses Binary Search not to find a specific target value, but to find the first index that satisfies a condition (the "gap" between value and index being $\ge k$).

---

## 🏃 Dry Run
**Input:** `arr = [2, 3, 4, 7, 11]`, `k = 5`

| Step | `low` | `high` | `mid` | `arr[mid]` | `missing` (`arr[mid]-(mid+1)`) | Action |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | 0 | 4 | 2 | 4 | $4 - (2+1) = \mathbf{1}$ | $1 < 5 \rightarrow$ `low = 3` |
| 2 | 3 | 4 | 3 | 7 | $7 - (3+1) = \mathbf{3}$ | $3 < 5 \rightarrow$ `low = 4` |
| 3 | 4 | 4 | 4 | 11 | $11 - (4+1) = \mathbf{6}$ | $6 \ge 5 \rightarrow$ `high = 3` |

**Loop Ends:** `low = 4`.
**Result:** `low + k` = `4 + 5` = **9**.
*(Missing numbers are: 1, 5, 6, 8, **9**, 10...)*

---

## ⚠️ Edge Cases
- **`k` is smaller than the first missing:** e.g., `arr=[5, 6]`, `k=2`. Result: `2`.
- **No numbers missing within the array range:** e.g., `arr=[1, 2, 3]`, `k=2`. Result: `5`.
- **Large gaps:** `arr=[1, 100]`, `k=10`. Result: `11`.

---

## 💡 Mistakes
> [!failure] **Common Pitfall: Linear Counting**
> **User Note:** *"dont understand the optimal approach"*
> 
> **Why Linear is slow:** Scanning one by one ($O(N)$) is intuitive but fails to use the **sorted** property.
> **The Fix:** Stop thinking about "counting" and start thinking about **"gaps"**.
> - At any index `i`, you *know* exactly how many numbers are missing before it. 
> - If `arr[10] = 20`, you know 9 numbers are missing ($20 - (10+1) = 9$). 
> - If you need the $5^{th}$ missing number, it must be to the left. If you need the $12^{th}$, it must be to the right. This "left or right" choice is the definition of **Binary Search**.

---

## 📊 Complexity
- **Time Complexity:** $O(\log N)$ — Binary search reduces the search space by half each time.
- **Space Complexity:** $O(1)$ — No extra data structures used.

---

## 🔗 Similar Problems
- [Missing Number](https://leetcode.com/problems/missing-number/)
- [Find the Duplicate Number](https://leetcode.com/problems/find-the-duplicate-number/)
- [First Missing Positive](https://leetcode.com/problems/first-missing-positive/)

#dsa #BinarySearch #leetcode

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-13)
- [ ] Day 7 Revision (2026-04-18)
- [ ] Day 15 Revision (2026-04-26)
- [ ] Day 30 Revision (2026-05-11)
