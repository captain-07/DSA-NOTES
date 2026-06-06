---
created: 2026-04-25
revisions:
  - 2026-04-27
  - 2026-05-02
  - 2026-05-10
  - 2026-05-25
---

# 2 Sum

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Google #Microsoft #Meta #Apple #Bloomberg #Adobe

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #hashmap [[Hash Map]], #array [[Arrays]], #searching [[Searching]]

---
## Pattern

Hash Map (Complement Tracking)

---
## Difficulty

Easy | #easy

---

## ⚡ Key Idea (Core Insight)

Instead of searching for two numbers that add up to `target`, iterate once and check if the **complement** (`target - current_value`) already exists in a Hash Map. This trades space for time, reducing a nested search to a constant time lookup.

---

## ⚡ Quick Recall (VERY IMPORTANT)

`Complement = Target - x`. Store `{value: index}` in a dictionary while traversing. If `Complement` is in the dictionary, you found the pair.

---

## Approach

### Brute Force
- Use nested loops to check every possible pair `(i, j)`.
- Time Complexity: $O(N^2)$

### Better
- Sort the array and use **Two Pointers** (left and right).
- Note: This returns values, not original indices (unless indices are stored before sorting).
- Time Complexity: $O(N \log N)$

### Optimal (One-Pass Hash Map)
1. Initialize an empty dictionary `prev_map`.
2. Iterate through `nums` with index `i` and value `n`.
3. Calculate `diff = target - n`.
4. If `diff` exists in `prev_map`, return `[prev_map[diff], i]`.
5. Otherwise, add `n` to `prev_map` as `{n: i}`.

---

## Code (Python)

```python
class Solution:
    def twoSum(self, nums: list[int], target: int) -> list[int]:
        # Dictionary to store value: index
        prev_map = {} 
        
        for i, n in enumerate(nums):
            diff = target - n
            
            # Check if the complement has been seen before
            if diff in prev_map:
                return [prev_map[diff], i]
            
            # Store current value and its index
            prev_map[n] = i
            
        return [] # Fallback if no solution exists
```

---

## Dry Run (Smart Example)

Input: `nums = [3, 2, -4, 8]`, `target = 4`

| Step | Current `n` | `diff` (4 - n) | `prev_map` (Before Step) | Action |
| :--- | :--- | :--- | :--- | :--- |
| 1 | 3 | 1 | `{}` | `diff` not in map. Add `{3: 0}` |
| 2 | 2 | 2 | `{3: 0}` | `diff` not in map. Add `{2: 1}` |
| 3 | -4 | 8 | `{3: 0, 2: 1}` | `diff` not in map. Add `{-4: 2}` |
| 4 | 8 | -4 | `{3: 0, 2: 1, -4: 2}` | **Match!** Return `[prev_map[-4], 3]` -> `[2, 3]` |

---

## Edge Cases

- **Negative Numbers:** Handled naturally by the math (`target - (-n)`).
- **Duplicates:** Handled correctly because the match is found before the second duplicate overwrites the first in the map.
- **Target is double a value:** e.g., `nums=[3, 4], target=6`. The logic ensures we don't use the same index twice because the check happens *before* the current index is added to the map.
- **No Solution:** Return empty list or null (as per constraints).

---

## Mistakes

- Trying to sort the array when original **indices** are required.
- Adding the current number to the hash map *before* checking the complement (can result in using the same element twice).
- **User Mistake:** No specific note provided (Ensure to document the "why" and "how" of the chosen approach).

---

## Complexity

Time: $O(N)$ → Single pass through the array.  
Space: $O(N)$ → Worst case stores all elements in the hash map.

---

## Similar Problems

- [2 Sum II - Input Array Is Sorted](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/) - Medium
- [3 Sum](https://leetcode.com/problems/3sum/) - Medium
- [4 Sum](https://leetcode.com/problems/4sum/) - Medium
- [Subarray Sum Equals K](https://leetcode.com/problems/subarray-sum-equals-k/) - Medium

---

## Tags and Properties
- #dsa #important #revisit #hashmap #blind75 [[Hash Map]] [[Arrays]]
- **Revision Date:** 2026-04-25
- **Problem Link:** [LeetCode - 2 Sum](https://leetcode.com/problems/two-sum/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-27)
- [ ] Day 7 Revision (2026-05-02)
- [ ] Day 15 Revision (2026-05-10)
- [ ] Day 30 Revision (2026-05-25)
