---
created: 2026-04-11
revisions:
  - 2026-04-13
  - 2026-04-18
  - 2026-04-26
  - 2026-05-11
---

# Two Sum

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Google #Microsoft #Adobe #Apple #Facebook #Uber

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #hashmap [[HashMap]], #array [[Arrays]], #searching [[Searching]]

## Pattern

Complement Search + HashMap

---
## Difficulty

Easy  
#easy

---

## ⚡ Key Idea (Core Insight)

Instead of searching for two numbers, iterate once and look for the **complement** (`target - current_value`) in a hash map. This converts a search problem from $O(N)$ to $O(1)$ lookup.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Store `value: index` in a map. For each `x`, if `target - x` is in the map, you've found the pair.

---

## Approach

### Brute Force
- Use two nested loops to check every possible pair `(i, j)` where `i != j`.
- **Time Complexity:** $O(N^2)$

### Optimal (One-Pass Hash Map)
- Maintain a dictionary `seen` to map values to their indices.
- For each number `num` at index `i`:
    1. Calculate `diff = target - num`.
    2. If `diff` exists in `seen`, return `[seen[diff], i]`.
    3. Otherwise, add `num` to `seen` with index `i`.
- **Time Complexity:** $O(N)$

---

## Code (Python)

```python
class Solution:
    def twoSum(self, nums: list[int], target: int) -> list[int]:
        # Map to store number: index
        seen = {}
        
        for i, num in enumerate(nums):
            complement = target - num
            
            # Check if complement was already encountered
            if complement in seen:
                return [seen[complement], i]
            
            # Store current number and its index
            seen[num] = i
            
        return [] # Should not happen per constraints
```

---

## Dry Run (Smart Example)

**Input:** `nums = [3, 2, 4]`, `target = 6`

| Step | Variables | Explanation |
| :--- | :--- | :--- |
| 1 | `i=0, num=3, diff=3` | `3` not in `seen`. Add `{3: 0}`. |
| 2 | `i=1, num=2, diff=4` | `4` not in `seen`. Add `{3: 0, 2: 1}`. |
| 3 | `i=2, num=4, diff=2` | `2` is in `seen` at index `1`. Return `[1, 2]`. |

---

## Edge Cases

- **Duplicates:** `[3, 3], target=6` (Ensure you don't use the same index twice).
- **Negative Numbers:** `[-1, -2, -3], target=-5` (Logic remains identical).
- **Large Inputs:** Hash map handles $O(N)$ efficiently without timeout.
- **First/Last Pair:** `[1, 5, 8], target=9` (Algorithm catches extremes).

---

## Mistakes

- **Using the same element twice:** Forgetting that an element cannot be reused unless it appears twice in the array.
- **Sorting first:** Sorting loses the original indices, requiring extra $O(N)$ space to store index-value pairs.
- **Initial test:** Basic sanity check of the environment and logic.

---

## Complexity

Time: $O(N)$ → Single pass through the array.  
Space: $O(N)$ → In the worst case, we store almost all elements in the hash map.

---

## Similar Problems

- [Two Sum II - Input Array Is Sorted](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/) - Medium
- [3Sum](https://leetcode.com/problems/3sum/) - Medium
- [4Sum](https://leetcode.com/problems/4sum/) - Medium
- [Subarray Sum Equals K](https://leetcode.com/problems/subarray-sum-equals-k/) - Medium

---

## Tags and Properties
  - #dsa #important #revisit  
  - #hashmap #arrays #leetcode1  
  - [[HashMap]] [[Arrays]] [[Searching]]
  - **Revision Date:** 2026-04-11
  - **Problem Link:** [LeetCode - Two Sum](https://leetcode.com/problems/two-sum/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-13)
- [ ] Day 7 Revision (2026-04-18)
- [ ] Day 15 Revision (2026-04-26)
- [ ] Day 30 Revision (2026-05-11)
