---
created: 2026-07-10
revisions:
  - 2026-07-12
  - 2026-07-17
  - 2026-07-25
  - 2026-08-09
---

# Two Sum

---

## Metadata & Placement Tags

- **Target Companies:** #Amazon #Google #Microsoft #Meta #Apple #Netflix
- **Confidence Checklist:**
  - [ ] Low
  - [ ] Medium
  - [ ] High

- **Concepts:** #hashmap [[HashMap]], #arrays [[Array]], #twopointers [[Two Pointers]]

---
## Pattern

HashMap (Complement Lookup)

---
## Difficulty

Easy
#easy

---
## ⚡ Key Idea (Core Insight)

For each number `x`, check if its complement `target - x` has already been visited and stored in a hash map. This converts a search problem from $O(N)$ to $O(1)$ lookup time.

---
## ⚡ Quick Recall (VERY IMPORTANT)

Store `target - nums[i]` as the key and index `i` as the value in a hash map while iterating.

---
## Approach

### Brute Force
- Check all pairs using nested loops to find if `nums[i] + nums[j] == target`.
- Time Complexity: $O(N^2)$
- Space Complexity: $O(1)$

### Better
- Store elements along with original indices, sort the array, and use a two-pointer approach.
- Time Complexity: $O(N \log N)$
- Space Complexity: $O(N)$

### Optimal
- Iterate through the array once.
- For each element, calculate `complement = target - num`.
- If `complement` exists in the hash map, return its stored index and the current index.
- Otherwise, insert the current element and its index into the map.
- Time Complexity: $O(N)$
- Space Complexity: $O(N)$

---
## Code (Python)

```python
class Solution:
    def twoSum(self, nums: list[int], target: int) -> list[int]:
        # Map to store number to its index
        seen = {}

        for i, num in enumerate(nums):
            complement = target - num
            # Check if complement already exists in map
            if complement in seen:
                return [seen[complement], i]
            # Store the current number with its index
            seen[num] = i

        return []
```

---
## Dry Run (Smart Example)

Input: `nums = [3, -1, 3, 4]`, `target = 6`

| Step | Variables | Explanation |
| :--- | :--- | :--- |
| 1 | `i = 0`, `num = 3`, `complement = 3`, `seen = {}` | `3` is not in `seen`. Add `{3: 0}`. |
| 2 | `i = 1`, `num = -1`, `complement = 7`, `seen = {3: 0}` | `7` is not in `seen`. Add `{-1: 1}`. |
| 3 | `i = 2`, `num = 3`, `complement = 3`, `seen = {3: 0, -1: 1}` | `3` is in `seen`. Return `[seen[3], 2]` -> `[0, 2]`. |

---
## Edge Cases

- **Negative Numbers:** e.g., `nums = [-3, 4, 3, 90]`, `target = 0` (correctly handles complement of negative numbers).
- **Duplicate Elements:** e.g., `nums = [3, 3]`, `target = 6` (handles duplicate complements on lookup before map overwrite).
- **Multiple Pairs:** Return the first valid pair found.
- **No Solution:** LeetCode guarantees exactly one solution, but return empty list as fallback.

---
## Mistakes

- Forgot hash map approach and tried sorting first (which loses index positions unless tracked).
- Trying to add the element to the hash map *before* checking the complement (results in using the same element twice, e.g., `nums = [3, 2, 4], target = 6` returning `[0, 0]`).

---
## Complexity

Time: O(N) → We traverse the array of size N only once. Hash map lookups are O(1) on average.
Space: O(N) → In the worst case, we store N elements in the hash map.

---
## Similar Problems

- [3Sum](https://leetcode.com/problems/3sum/) - Medium
- [4Sum](https://leetcode.com/problems/4sum/) - Medium
- [Two Sum II - Input Array Is Sorted](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/) - Medium
- [Subarray Sum Equals K](https://leetcode.com/problems/subarray-sum-equals-k/) - Medium

---
## Tags and Properties

- #dsa #important #revisit #hashmap #arrays
- Obsidian links: [[HashMap]], [[Array]], [[Two Pointers]]
- **Revision Date:** 2026-07-10
- **Problem Link:** [LeetCode - Two Sum](https://leetcode.com/problems/two-sum/)

---

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-07-12)
- [ ] Day 7 Revision (2026-07-17)
- [ ] Day 15 Revision (2026-07-25)
- [ ] Day 30 Revision (2026-08-09)
