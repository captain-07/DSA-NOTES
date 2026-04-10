---
created: 2026-04-10
revisions:
  - 2026-04-12
  - 2026-04-17
  - 2026-04-25
  - 2026-05-10
---

# Two Sum

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Google #Microsoft #Meta #Apple #Adobe #Uber

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #hashmap [[HashMap]], #array [[Array]]

## Pattern

HashMap (One-pass)

---
## Difficulty

Easy #easy

---

## ⚡ Key Idea (Core Insight)

- For every number `x`, we are looking for a `complement` such that `complement = target - x`.
- A HashMap stores previously seen numbers as keys and their indices as values, enabling $O(1)$ lookups for the complement.

---

## ⚡ Quick Recall (VERY IMPORTANT)

- Iterate once: `if target - num in seen: return [seen[target - num], current_index]`. 
- Store current number in map **after** checking to prevent using the same element twice.

---

## Approach

### Brute Force
- Use nested loops to check every possible pair $(i, j)$ where $i \neq j$.
- Time: $O(n^2)$ | Space: $O(1)$

### Optimal (One-Pass Hash Map)
1. Initialize an empty hash map `prev_map`.
2. Iterate through `nums` with index `i`.
3. Calculate `diff = target - nums[i]`.
4. If `diff` exists in `prev_map`, return `[prev_map[diff], i]`.
5. Otherwise, add `nums[i]` to `prev_map` with its index `i`.
- Time: $O(n)$ | Space: $O(n)$

---

## Code (Python)

```python
class Solution:
    def twoSum(self, nums: list[int], target: int) -> list[int]:
        # prev_map: value -> index
        prev_map = {}
        
        for i, n in enumerate(nums):
            diff = target - n
            # Check if complement exists in map
            if diff in prev_map:
                return [prev_map[diff], i]
            
            # Store current value and index for future complements
            prev_map[n] = i
            
        return [] # Should not happen based on constraints
```

---

## Dry Run (Smart Example)

**Input:** `nums = [3, 2, 4], target = 6`

| Step | Variables | Explanation |
| :--- | :--- | :--- |
| 1 | `i=0, n=3, diff=3, map={}` | `3` not in map. Add `3: 0` to map. |
| 2 | `i=1, n=2, diff=4, map={3: 0}` | `4` not in map. Add `2: 1` to map. |
| 3 | `i=2, n=4, diff=2, map={3:0, 2:1}` | `2` IS in map! Return `[prev_map[2], 2]`. |
| **Result** | **[1, 2]** | Indices of 2 and 4. |

---

## Edge Cases

- **Duplicates:** `[3, 3], target=6` (Ensure second 3 finds the first 3 in the map).
- **Negative Numbers:** `[-1, -2, -3], target=-5` (Logic remains same).
- **Target is double a number:** `[3, 2, 4], target=6` (Must not return index `0` twice for `3+3`).
- **Large Inputs:** Ensure $O(n)$ to avoid TLE.

---

## Mistakes

- **Same Element Twice:** Accessing the same index twice (e.g., `target=6`, `nums=[3, 2]`, returning `[0, 0]`). *[User Mistake]*
- **Map Update Timing:** Adding the current number to the map **before** checking for the complement (causes the "same element" bug).
- **Sorting First:** Sorting `nums` breaks the original index mapping unless pairs of `(value, index)` are stored.

---

## Complexity

Time: $O(n)$ → Single pass through the array.  
Space: $O(n)$ → Worst case stores all elements in the hash map.

---

## Similar Problems

- [Two Sum II - Input Array Is Sorted](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/) - Medium
- [3Sum](https://leetcode.com/problems/3sum/) - Medium
- [4Sum](https://leetcode.com/problems/4sum/) - Medium
- [Subarray Sum Equals K](https://leetcode.com/problems/subarray-sum-equals-k/) - Medium

---

## Tags and Properties
- #dsa #important #revisit  
- #hashmap #array #blind75 
- [[HashMap]] [[Array]]
- **Revision Date:** 2026-04-10
- **Problem Link:** [LeetCode - Two Sum](https://leetcode.com/problems/two-sum/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-12)
- [ ] Day 7 Revision (2026-04-17)
- [ ] Day 15 Revision (2026-04-25)
- [ ] Day 30 Revision (2026-05-10)
