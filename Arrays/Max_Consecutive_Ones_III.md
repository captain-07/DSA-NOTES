---
created: 2026-08-11
revisions:
  - 2026-08-13
  - 2026-08-18
  - 2026-08-26
  - 2026-09-10
---

# Max Consecutive Ones III

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Google #Amazon #Microsoft #Adobe #Uber

- **Confidence Checklist:**
  - [ ] Low
  - [ ] Medium
  - [ ] High

- **Concepts:**
  - #arrays [[Arrays]]
  - #slidingwindow [[Sliding Window]]
  - #twopointers [[Two Pointers]]

## Pattern

Sliding Window (Variable Size, Shrinking)

---
## Difficulty

Medium
#medium

---

## ⚡ Key Idea (Core Insight)

Find the longest subarray containing at most `k` zeros. Instead of shrinking on distinct values, track the count of zeros inside the window; when it exceeds `k`, move the left pointer until it is valid again.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Longest subarray with at most `k` zeros. Expand `right`, count zeros. While `zero_count > k`, shift `left` (and decrement zero count if `nums[left] == 0`). Track `right - left + 1`.

---

## Approach

### Brute Force
Check every subarray and count the zeros in each; keep the longest one that has at most `k` zeros.
- **Time Complexity:** O(N²)
- **Space Complexity:** O(1)

### Optimal: Sliding Window
1. Expand `right` one step at a time.
2. If `nums[right] == 0`, increment `zero_count`.
3. While `zero_count > k`, shrink from the left: if `nums[left] == 0`, decrement `zero_count`; always increment `left`.
4. Window is always valid, so update the answer with `max(max_len, right - left + 1)`.
- **Time Complexity:** O(N)
- **Space Complexity:** O(1)

---

## Code (Python)

```python
class Solution:
    def longestOnes(self, nums: list[int], k: int) -> int:
        left = 0
        zero_count = 0
        max_len = 0

        for right in range(len(nums)):
            if nums[right] == 0:
                zero_count += 1

            while zero_count > k:
                if nums[left] == 0:
                    zero_count -= 1
                left += 1

            max_len = max(max_len, right - left + 1)

        return max_len
```

---

## Dry Run (Smart Example)

**Input:** `nums = [1, 1, 1, 0, 0, 0, 1, 1, 1, 1, 0]`, `k = 2`

| Step | `right` | `nums[right]` | `zero_count` | `left` | `max_len` | Explanation |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | 0 | 1 | 0 | 0 | 1 | Valid window `[1]`. |
| 2 | 1 | 1 | 0 | 0 | 2 | Valid window `[1, 1]`. |
| 3 | 2 | 1 | 0 | 0 | 3 | Valid window `[1, 1, 1]`. |
| 4 | 3 | 0 | 1 | 0 | 4 | `k = 2`, still valid. |
| 5 | 4 | 0 | 2 | 0 | 5 | `k = 2`, still valid. |
| 6 | 5 | 0 | 3 | 1 | 5 | `zero_count > 2`. Shrink: drop `nums[0]=1`, `left=1`. |
| 7 | 6 | 1 | 3 | 2 | 5 | Shrink: drop `nums[1]=1`, `left=2`. |
| 8 | 7 | 1 | 3 | 3 | 5 | Shrink: drop `nums[2]=1`, `left=3`. |
| 9 | 8 | 1 | 2 | 3 | 6 | Now valid. `[0, 0, 1, 1, 1, 1]`. |
| 10 | 9 | 1 | 2 | 3 | 7 | Window grows. `[0, 0, 1, 1, 1, 1, 1]`. |
| 11 | 10 | 0 | 3 | 4 | 7 | Shrink: drop `nums[3]=0`, `zero_count=2`, `left=4`. |

Final answer: `7`.

---

## Edge Cases

- **k = 0:** Reduces to finding the longest run of consecutive 1s.
- **All Zeros:** With `k = len(nums)`, the whole array is valid; answer is `N`.
- **k >= Number of Zeros:** The entire array is a valid window; answer is `N`.
- **Single Element:** `[0]` with `k = 1` returns 1; `[0]` with `k = 0` returns 0.

---

## Mistakes

- **Shrinking with `if` instead of `while`:** Multiple zeros may need to be dropped; a single shrink is not enough.
- **Forgetting to move `left` on every shrink iteration:** The `while` loop must always increment `left` to actually shrink the window.
- **Counting zeros inside `nums[left]` when it is not zero:** Only decrement `zero_count` when the element leaving the window is actually a `0`.

---

## Complexity

Time: O(N) → Each element is visited at most twice (once by `right`, once by `left`).  
Space: O(1) → Only a few integer variables are used.

---

## Similar Problems

- [Max Consecutive Ones](https://leetcode.com/problems/max-consecutive-ones/) - Easy
- [Max Consecutive Ones II](https://leetcode.com/problems/max-consecutive-ones-ii/) - Medium
- [Longest Substring with At Most K Distinct Characters](https://leetcode.com/problems/longest-substring-with-at-most-k-distinct-characters/) - Medium
- [Fruit Into Baskets](https://leetcode.com/problems/fruit-into-baskets/) - Medium

---

## Tags and Properties
  - #dsa #important #revisit
  - #slidingwindow #two-pointers #array-streak
  - [[Arrays]] [[Sliding Window]] [[Two Pointers]]
  - **Revision Date:** 2026-08-11
  - **Problem Link:** [LeetCode - Max Consecutive Ones III](https://leetcode.com/problems/max-consecutive-ones-iii/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-08-13)
- [ ] Day 7 Revision (2026-08-18)
- [ ] Day 15 Revision (2026-08-26)
- [ ] Day 30 Revision (2026-09-10)