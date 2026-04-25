---
created: 2026-04-25
revisions:
  - 2026-04-27
  - 2026-05-02
  - 2026-05-10
  - 2026-05-25
---

# Maximum Consecutive Ones

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Google #Microsoft #Meta #Apple

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #arrays [[Arrays]]
  - #slidingwindow [[Sliding Window]]
  - #iteration [[Iteration]]

## Pattern

Linear Scan / Single Pass Counting

---
## Difficulty

Easy
#easy

---

## ⚡ Key Idea (Core Insight)

Maintain a running `current_count` of consecutive 1s. Every time a `1` is encountered, increment the counter and update the `global_max`. When a `0` is encountered, reset the `current_count` to zero.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Increment counter on `1`, reset to `0` on `0`, update `max` at every `1`.

---

## Approach

### Brute Force
- Generate all possible subarrays, check if they contain only 1s, and track the length of the longest one.
- **Time Complexity:** O(N²)

### Optimal
- Iterate through the array once.
- Use a `count` variable to track the current streak of 1s.
- Use a `max_count` variable to store the highest `count` seen.
- Reset `count = 0` whenever `nums[i] == 0`.

---

## Code (Python)

```python
class Solution:
    def findMaxConsecutiveOnes(self, nums: list[int]) -> int:
        max_count = 0
        current_count = 0
        
        for num in nums:
            if num == 1:
                current_count += 1
                # Update global maximum if current streak is higher
                if current_count > max_count:
                    max_count = current_count
            else:
                # Sequence broken by a 0, reset streak
                current_count = 0
                
        return max_count
```

---

## Dry Run (Smart Example)

**Input:** `nums = [1, 0, 1, 1, 0, 1]`

| Step | Num | `current_count` | `max_count` | Explanation |
| :--- | :--- | :--- | :--- | :--- |
| 1 | 1 | 1 | 1 | Encountered 1, increment count, update max. |
| 2 | 0 | 0 | 1 | Encountered 0, reset count. Max stays 1. |
| 3 | 1 | 1 | 1 | Encountered 1, count = 1. |
| 4 | 1 | 2 | 2 | Encountered 1, count = 2, update max. |
| 5 | 0 | 0 | 2 | Encountered 0, reset count. Max stays 2. |
| 6 | 1 | 1 | 2 | Encountered 1, count = 1. Max stays 2. |

---

## Edge Cases

- **Empty Array:** Should return 0 (if constraints allow empty, though usually `n >= 1`).
- **All Zeros:** `current_count` stays 0, `max_count` returns 0.
- **All Ones:** `current_count` increments until the end, returns array length.
- **Single Element:** Returns 1 if `[1]`, 0 if `[0]`.

---

## Mistakes

- **Updating max only at the end:** If the array ends with 1s, and you only update `max` when you hit a `0`, you might miss the final streak. (Update inside the `if num == 1` block).
- **Off-by-one errors:** Ensure the counter starts at 0 and increments correctly.
- **User Mistake:** No specific note provided.

---

## Complexity

Time: O(N) → We traverse the array exactly once.  
Space: O(1) → We only use two integer variables (`max_count`, `current_count`).

---

## Similar Problems

- [Max Consecutive Ones II](https://leetcode.com/problems/max-consecutive-ones-ii/) - Medium
- [Max Consecutive Ones III](https://leetcode.com/problems/max-consecutive-ones-iii/) - Medium
- [Consecutive Characters](https://leetcode.com/problems/consecutive-characters/) - Easy
- [Longest Turbulent Subarray](https://leetcode.com/problems/longest-turbulent-subarray/) - Medium

---

## Tags and Properties
  - #dsa #important #revisit  
  - #array-streak #linear-scan
  - [[Arrays]] [[Sliding Window]]
  - **Revision Date:** 2026-04-25
  - **Problem Link:** [LeetCode - Max Consecutive Ones](https://leetcode.com/problems/max-consecutive-ones/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-27)
- [ ] Day 7 Revision (2026-05-02)
- [ ] Day 15 Revision (2026-05-10)
- [ ] Day 30 Revision (2026-05-25)
