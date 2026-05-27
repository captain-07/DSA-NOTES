---
created: 2026-05-27
revisions:
  - 2026-05-29
  - 2026-06-03
  - 2026-06-11
  - 2026-06-26
---

# Two Sum

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Google #Microsoft #Adobe #Apple #Meta

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #hashmap [[Hash Map]]
  - #array [[Array]]

## Pattern

HashMap (Complement Search)

---
## Difficulty

Easy  
#easy

---

## ⚡ Key Idea (Core Insight)

For any number `x`, we are looking for a complement `y` such that `y = target - x`. Instead of re-scanning the array for `y`, store each visited number and its index in a **HashMap** to achieve $O(1)$ average lookups.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Store "Value -> Index" in a Map. For each item, check if `target - current` exists in the Map before adding the current item to the Map.

---

## Approach

### Brute Force
- Nested loops: Check every pair $(i, j)$ to see if `nums[i] + nums[j] == target`.
- Time: $O(n^2)$ | Space: $O(1)$

### Optimal (One-Pass Hash Map)
- Iterate through the array once.
- Calculate `complement = target - nums[i]`.
- If `complement` exists in the Map, return `[Map[complement], i]`.
- Otherwise, add `nums[i]` to the Map.
- **Why it works:** By checking the Map *before* adding the current element, we automatically avoid using the same index twice.

---

## Code (Python)

```python
class Solution:
    def twoSum(self, nums: list[int], target: int) -> list[int]:
        # Stores value -> index mapping
        prev_map = {}
        
        for i, n in enumerate(nums):
            diff = target - n
            
            # Check if the needed complement was already seen
            if diff in prev_map:
                # Return index of stored complement and current index
                return [prev_map[diff], i]
            
            # Store current value and its index
            prev_map[n] = i
        
        return [] # Guaranteed one solution exists
```

---

## Dry Run (Smart Example)

**Input:** `nums = [3, 4, 2], target = 6`

| Step | Variables | Explanation |
| :--- | :--- | :--- |
| 1 | `i=0, n=3, diff=3` | `prev_map` is `{}`. `3` not in map. Add `{3: 0}`. |
| 2 | `i=1, n=4, diff=2` | `prev_map` is `{3: 0}`. `2` not in map. Add `{3: 0, 4: 1}`. |
| 3 | `i=2, n=2, diff=4` | `prev_map` is `{3: 0, 4: 1}`. `4` is found at index `1`. |
| 4 | **Result** | Return `[1, 2]`. |

---

## Edge Cases

- **Negative Numbers:** `nums = [-3, 4, 3, 90], target = 0` → Returns `[0, 2]`.
- **Target is double an element:** `nums = [3, 2, 4], target = 6` → Must return `[1, 2]`, not `[0, 0]`.
- **Duplicates:** `nums = [3, 3], target = 6` → Returns `[0, 1]`.
- **No Solution:** (Not applicable per LeetCode constraints, but handle with empty list/exception).

---

## Mistakes

- **Forgot to check for same index:** If using a two-pass approach, you might return the same index twice (e.g., `target=6, nums[0]=3`, map finds index 0). One-pass avoids this naturally.
- **Sorting First:** $O(n \log n)$ is sub-optimal and loses original index positions.
- **Returning Values:** Ensure indices are returned, not the numbers themselves.

---

## Complexity

Time: $O(n)$ → Single pass with $O(1)$ hash map operations.  
Space: $O(n)$ → Map stores up to $n$ elements.

---

## Similar Problems

- [Two Sum II - Input Array Is Sorted](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/) - Easy
- [3Sum](https://leetcode.com/problems/3sum/) - Medium
- [4Sum](https://leetcode.com/problems/4sum/) - Medium
- [Subarray Sum Equals K](https://leetcode.com/problems/subarray-sum-equals-k/) - Medium

---

## Tags and Properties
  - #dsa #important #revisit  
  - #hashing [[Hashing]] #blind75
  - **Revision Date:** 2026-05-27
  - **Problem Link:** [LeetCode - Two Sum](https://leetcode.com/problems/two-sum/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-05-29)
- [ ] Day 7 Revision (2026-06-03)
- [ ] Day 15 Revision (2026-06-11)
- [ ] Day 30 Revision (2026-06-26)
