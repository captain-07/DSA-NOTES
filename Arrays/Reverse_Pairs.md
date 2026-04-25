---
created: 2026-04-25
revisions:
  - 2026-04-27
  - 2026-05-02
  - 2026-05-10
  - 2026-05-25
---

# Reverse Pairs

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Google #Amazon #Microsoft #Adobe #Cisco

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #DivideAndConquer [[Divide and Conquer]]
  - #MergeSort [[Merge Sort]]
  - #TwoPointers [[Two Pointers]]
  - #BIT [[Fenwick Tree]]

---
## Pattern

Modified Merge Sort (Count-while-Merge)

---
## Difficulty

Hard
#hard

---
## ⚡ Key Idea (Core Insight)

The problem asks for pairs $(i, j)$ where $i < j$ and $nums[i] > 2 \times nums[j]$. Like standard Inversion Count, we leverage **Merge Sort**. While merging two sorted halves, we use a **Two-Pointer** approach to count valid pairs *before* performing the actual merge, taking advantage of the sorted property.

---
## ⚡ Quick Recall (VERY IMPORTANT)

Perform a standard Merge Sort. In the merge step, before merging, use two pointers $i$ (left half) and $j$ (right half) to count how many $nums[i] > 2 \times nums[j]$ exist.

---
## Approach

### Brute Force
- Nested loops checking every pair $(i, j)$ where $i < j$.
- Time: $O(N^2)$
- Space: $O(1)$

### Better (BIT/Segment Tree)
- Coordinate compression + Fenwick Tree. Traverse from right to left, query counts, and update.
- Time: $O(N \log N)$
- Space: $O(N)$

### Optimal (Merge Sort)
1. Recursively divide the array into halves.
2. In the `count_and_merge` step:
   - **Count:** For each element in `left_half`, move pointer `j` in `right_half` as long as `nums[i] > 2 * nums[j]`. Total count += $j - (start\_of\_right\_half)$.
   - **Merge:** Standard sorted merge of the two halves.
- Time: $O(N \log N)$
- Space: $O(N)$

---
## Code (Python)

```python
class Solution:
    def reversePairs(self, nums: list[int]) -> int:
        return self.merge_sort(nums, 0, len(nums) - 1)

    def merge_sort(self, nums: list[int], low: int, high: int) -> int:
        if low >= high:
            return 0
        
        mid = (low + high) // 2
        count = self.merge_sort(nums, low, mid)
        count += self.merge_sort(nums, mid + 1, high)
        
        # Count pairs before merging
        count += self.count_pairs(nums, low, mid, high)
        
        # Standard Merge
        nums[low:high + 1] = sorted(nums[low:high + 1])
        return count

    def count_pairs(self, nums: list[int], low: int, mid: int, high: int) -> int:
        right = mid + 1
        total = 0
        for i in range(low, mid + 1):
            # Move right pointer while condition holds
            while right <= high and nums[i] > 2 * nums[right]:
                right += 1
            total += (right - (mid + 1))
        return total
```

---
## Dry Run (Smart Example)

Input: `nums = [1, 3, 2, 3, 1]`

| Step | Sub-arrays (Sorted) | Variables | Explanation |
| :--- | :--- | :--- | :--- |
| 1 | `[1, 3]` and `[2]` | `i=1 (val:3), j=2 (val:2)` | `3 > 2*2` is False. Count: 0. |
| 2 | `[3]` and `[1]` | `i=3 (val:3), j=4 (val:1)` | `3 > 2*1` is True. Count: 1. |
| 3 | `[1, 2, 3]` and `[1, 3]` | `i=0, j=3` | `1 > 2*1` (F); `i=1, 2 > 2*1` (F); `i=2, 3 > 2*1` (T). |
| 4 | Final Count | `Total = 2` | Pairs: `(3, 1)` at indices `(1, 4)` and `(3, 4)`. |

---
## Edge Cases

- **Empty / Single Element:** Return 0.
- **Negative Numbers:** Condition $nums[i] > 2 \times nums[j]$ still applies (e.g., $-1 > 2 \times -2$).
- **Large Values:** Python handles large integers; in C++, use `long long` for $2 \times nums[j]$.
- **All Identical:** If all same, count is 0 unless values are negative.

---
## Mistakes

- **Incorrect Condition:** Using `nums[i] >= 2 * nums[j]` instead of `>`.
- **Counting During Merge:** Standard inversion count adds to result *during* the merge; here, you MUST count *before* merging because the $2 \times$ condition breaks the standard logic.
- **User Mistake:** No specific note provided (ensure you track why the two-pointer works on sorted halves).

---
## Complexity

Time: O(N log N) → Each level of recursion takes $O(N)$ for counting and merging.  
Space: O(N) → Due to temporary arrays used during the merge process.

---
## Similar Problems

- [Count of Inversions](https://www.geeksforgeeks.org/inversion-count-in-array-using-merge-sort/) - Medium
- [Count of Smaller Numbers After Self](https://leetcode.com/problems/count-of-smaller-numbers-after-self/) - Hard
- [Create Maximum Number](https://leetcode.com/problems/create-maximum-number/) - Hard
- [Global and Local Inversions](https://leetcode.com/problems/global-and-local-inversions/) - Medium

---
## Tags and Properties
- #dsa #important #revisit
- #mergesort [[Merge Sort]]
- #divideandconquer [[Divide and Conquer]]
- **Problem Link:** [LeetCode Reverse Pairs](https://leetcode.com/problems/reverse-pairs/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-27)
- [ ] Day 7 Revision (2026-05-02)
- [ ] Day 15 Revision (2026-05-10)
- [ ] Day 30 Revision (2026-05-25)
