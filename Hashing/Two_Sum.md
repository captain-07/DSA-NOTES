---
created: 2026-09-13
revisions:
  - 2026-09-15
  - 2026-09-20
  - 2026-09-28
  - 2026-10-13
---

# Two Sum

---

## Metadata & Placement Tags

- **Folder:** Hashing
- **Target Companies:** #Amazon #Google #Microsoft #Facebook #Apple
- **Confidence Checklist:**
  - [ ] Low
  - [ ] Medium
  - [ ] High

- **Concepts:** #hashmap [[HashMap]], #array [[Array]]

---
## Pattern

Hash Map Lookups / Complement Search

---
## Difficulty

Easy | #easy

---

## ⚡ Key Idea (Core Insight)

For each element `num`, its required pair is `target - num`. Store each visited element and its index in a Hash Map to check for the complement in $O(1)$ constant time.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Store `(value -> index)` in Hash Map. For current number, check if `target - current` already exists in map.

---

## Approach

### Brute Force
- Check all pairs using two nested loops.
- Time: $O(N^2)$, Space: $O(1)$

### Optimal
1. Initialize an empty Hash Map `seen = {}`.
2. Iterate through the array with element `num` and index `index`.
3. Calculate `complement = target - num`.
4. If `complement` exists in `seen`, return `[seen[complement], index]`.
5. Otherwise, record current element: `seen[num] = index`.

---

## Code (Python)

```python
class Solution:
    def twoSum(self, nums: list[int], target: int) -> list[int]:
        # Hash map to store value -> index mapping
        seen_numbers = {}

        for current_index, current_number in enumerate(nums):
            complement = target - current_number

            # Check if complement already exists in map
            if complement in seen_numbers:
                return [seen_numbers[complement], current_index]

            # Store index of the current number
            seen_numbers[current_number] = current_index

        return []
```

---

## Dry Run (Smart Example)

Input: `nums = [3, -1, 4, 7]`, `target = 6`

| Step | Variables | Explanation |
| :--- | :--- | :--- |
| 1 | `i=0, num=3, complement=3` | `3` not in `seen`. Add `{3: 0}`. |
| 2 | `i=1, num=-1, complement=7` | `7` not in `seen`. Add `{-1: 1}`. |
| 3 | `i=2, num=4, complement=2` | `2` not in `seen`. Add `{4: 2}`. |
| 4 | `i=3, num=7, complement=-1` | `-1` found in `seen` at index `1`. Return `[1, 3]`. |

---

## Edge Cases

- **Negative Numbers:** Handled naturally by arithmetic subtraction `target - num`.
- **Duplicate Values:** `target` formed by duplicate values (e.g. `[3, 3]`, `target=6`); map lookup finds previous instance before current is stored.
- **No Solution:** Returns `[]` if no valid pair exists.

---

## Mistakes

- No specific note provided.
- Inserting the current element into the Hash Map *before* checking for the complement (can mistakenly match an element with itself when `target = 2 * num`).
- Returning values instead of 0-based indices as required.

---

## Complexity

Time: $O(N)$ → Single pass through the list with $O(1)$ Hash Map lookups.
Space: $O(N)$ → Up to $N$ elements stored in the Hash Map.

---

## Similar Problems

- [Two Sum II - Input Array Is Sorted](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/) - Medium
- [3Sum](https://leetcode.com/problems/3sum/) - Medium
- [4Sum](https://leetcode.com/problems/4sum/) - Medium
- [Two Sum IV - Input is a BST](https://leetcode.com/problems/two-sum-iv-input-is-a-bst/) - Easy

---

## Tags and Properties

- #dsa #important #revisit
- #array #hashmap #twosum
- [[HashMap]] [[Array]]
- **Last Revised:** 2026-09-13
- **Problem Link:** [LeetCode - Two Sum](https://leetcode.com/problems/two-sum/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-09-15)
- [ ] Day 7 Revision (2026-09-20)
- [ ] Day 15 Revision (2026-09-28)
- [ ] Day 30 Revision (2026-10-13)
