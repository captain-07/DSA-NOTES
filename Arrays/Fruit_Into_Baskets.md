---
created: 2026-08-12
revisions:
  - 2026-08-14
  - 2026-08-19
  - 2026-08-27
  - 2026-09-11
---

# Fruit Into Baskets

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Google #Amazon #Microsoft #Uber #Leads

- **Confidence Checklist:**
  - [ ] Low
  - [ ] Medium
  - [ ] High

- **Concepts:**
  - #slidingwindow [[Sliding Window]], #hashmap [[HashMap]], #array [[Array]]

## Pattern
Two Pointers / Sliding Window (Variable Size)

---
## Difficulty
Medium #medium

---

## ⚡ Key Idea (Core Insight)

Find the length of the longest contiguous subarray containing at most 2 distinct integers. Use a sliding window with a frequency map to track and limit the unique elements to 2.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Longest subarray with at most 2 distinct elements. Expand `right`, insert to hash map. If `len(map) > 2`, shrink `left` and delete key if count hits 0.

---

## Approach

### Brute Force
Check all possible subarrays and count distinct elements using a set.
- Time Complexity: O(N^2)
- Space Complexity: O(N)

### Optimal 1: Standard Sliding Window (Shrinking)
Expand the window using `right`. If the map size exceeds 2, increment `left`, decrement counts, and delete key at count 0 until map size is at most 2.
- Time: O(N)
- Space: O(1)

### Optimal 2: Non-Shrinking Sliding Window
Instead of shrinking the window, we just shift it. If map size > 2, decrement the left element's count, remove if 0, and shift `left` by 1. The window size never decreases.
- Time: O(N)
- Space: O(1)

---

## Code (Python)

### Solution 1: Standard Sliding Window
```python
class Solution:
    def totalFruit(self, fruits: list[int]) -> int:
        count = {}
        left = 0
        max_fruits = 0

        for right in range(len(fruits)):
            count[fruits[right]] = count.get(fruits[right], 0) + 1

            # Shrink from left if distinct fruits > 2
            while len(count) > 2:
                count[fruits[left]] -= 1
                if count[fruits[left]] == 0:
                    del count[fruits[left]]
                left += 1

            max_fruits = max(max_fruits, right - left + 1)

        return max_fruits
```

### Solution 2: Non-Shrinking Window
```python
class Solution:
    def totalFruit(self, fruits: list[int]) -> int:
        count = {}
        left = 0

        for right in range(len(fruits)):
            count[fruits[right]] = count.get(fruits[right], 0) + 1

            if len(count) > 2:
                count[fruits[left]] -= 1
                if count[fruits[left]] == 0:
                    del count[fruits[left]]
                left += 1

        return len(fruits) - left
```

---

## Dry Run (Smart Example)

Input: `fruits = [1, 2, 3, 2, 2]`

| Step | Variables | Explanation |
| :--- | :--- | :--- |
| 1 | `right=0`, `left=0`, `count={1:1}`, `max=1` | Add `1`. Valid window. |
| 2 | `right=1`, `left=0`, `count={1:1, 2:1}`, `max=2` | Add `2`. Valid window. |
| 3 | `right=2`, `left=0`, `count={1:1, 2:1, 3:1}` -> `left=2`, `count={2:1, 3:1}` | Add `3`. Size > 2. Shrink left (removes 1). |
| 4 | `right=3`, `left=2`, `count={2:2, 3:1}`, `max=3` | Add `2`. Valid window `[3, 2, 2]`. |
| 5 | `right=4`, `left=2`, `count={2:3, 3:1}`, `max=4` | Add `2`. Valid window `[3, 2, 2, 2]`. |

---

## Edge Cases

- **Only 1 or 2 fruit types:** `[1, 1, 1]` or `[1, 2]` -> Returns full array size.
- **Alternating types:** `[1, 2, 1, 2, 1]` -> Never exceeds 2 distinct types; returns full size.
- **Strictly increasing types:** `[1, 2, 3, 4]` -> Window shifts continuously; returns 2.

---

## Mistakes

- **User Mistake:** No specific note provided.
- Failing to delete the key from the hash map when count reaches 0, which incorrectly keeps `len(count)` > 2.
- Shrinking the window with an `if` condition when using a standard variable sliding window that might need multiple shrinks (use `while` for standard implementation).

---

## Complexity

Time: O(N) → Each element is processed at most twice (once by `right` and once by `left`).
Space: O(1) → The hash map stores at most 3 distinct elements.

---

## Similar Problems

- [Longest Substring Without Repeating Characters](https://leetcode.com/problems/longest-substring-without-repeating-characters/) - Medium
- [Longest Substring with At Most K Distinct Characters](https://leetcode.com/problems/longest-substring-with-at-most-k-distinct-characters/) - Medium
- [Max Consecutive Ones III](https://leetcode.com/problems/max-consecutive-ones-iii/) - Medium

---

## Tags and Properties
- #dsa #important #revisit
- #slidingwindow #hashmap #two-pointers
- [[Sliding Window]], [[HashMap]], [[Two Pointers]]
- **Revision Date:** 2026-08-12
- **Problem Link:** [LeetCode - Fruit Into Baskets](https://leetcode.com/problems/fruit-into-baskets/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-08-14)
- [ ] Day 7 Revision (2026-08-19)
- [ ] Day 15 Revision (2026-08-27)
- [ ] Day 30 Revision (2026-09-11)
