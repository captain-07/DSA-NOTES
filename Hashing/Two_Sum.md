---
created: 2026-04-07
revisions:
  - 2026-04-09
  - 2026-04-14
  - 2026-04-22
  - 2026-05-07
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

HashMap (Complement Search)

---
## Difficulty

Easy  
#easy

---

## ⚡ Key Idea (Core Insight)

Instead of searching for a pair by nested iteration ($O(N^2)$), use a **HashMap** to store previously seen numbers and their indices. For each element $x$, calculate the required `complement = target - x` and check if it exists in the map in $O(1)$ time.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Store `index` of visited elements in a map. If `target - current` is in the map, you found the pair.

---

## Approach

### Brute Force
- Iterate through every pair $(i, j)$ and check if $nums[i] + nums[j] == target$.
- Time Complexity: $O(N^2)$

### Optimal (One-Pass Hash Map)
- Use a dictionary to store `{value: index}`.
- For each number, calculate `complement`.
- If `complement` is in the dictionary, return `[dictionary[complement], current_index]`.
- Otherwise, add the current number to the dictionary.

---

## Code (Python)

```python
def twoSum(nums, target):
    # Dictionary to store value -> index mapping
    prev_map = {} 
    
    for i, n in enumerate(nums):
        diff = target - n
        
        # Check if the required complement was already seen
        if diff in prev_map:
            return [prev_map[diff], i]
        
        # Store current number and its index for future lookups
        prev_map[n] = i
        
    return [] # Should not reach here based on problem constraints
```

---

## Dry Run (Smart Example)

**Input:** `nums = [3, 2, 4], target = 6`

| Step | Current (n) | Diff (6 - n) | prev_map (before update) | Explanation |
| :--- | :--- | :--- | :--- | :--- |
| 1 | 3 | 3 | `{}` | 3 not in map. Store `{3: 0}`. |
| 2 | 2 | 4 | `{3: 0}` | 4 not in map. Store `{3: 0, 2: 1}`. |
| 3 | 4 | 2 | `{3: 0, 2: 1}` | **2 is in map!** Return `[prev_map[2], 2]` -> `[1, 2]`. |

---

## Edge Cases

- **Negative Numbers:** `nums = [-1, -2, -3, -4], target = -5` → Works normally.
- **Multiple Pairs:** Return the first one found (standard LC behavior).
- **Large Inputs:** $O(N)$ ensures it won't Time Limit Exceeded (TLE).
- **Same Number as Complement:** `nums = [3, 3], target = 6` → Handled by storing after checking.

---

## Mistakes

- **Forgot to use HashMap:** Attempting $O(N^2)$ or unnecessary sorting.
- **Sorting First:** Changes original indices; requires storing original positions before sorting.
- **Handling Duplicates:** Returning the same index twice (e.g., for `target = 6, nums = [3]`).
- **One-pass vs Two-pass:** One-pass is cleaner and handles duplicates naturally.

---

## Complexity

Time: $O(N)$ → We traverse the list containing $N$ elements exactly once. Each lookup in the table costs only $O(1)$ time.  
Space: $O(N)$ → In the worst case, we store all $N$ elements in the hash table.

---

## Similar Problems

- [3Sum](https://leetcode.com/problems/3sum/) - Medium
- [Two Sum II - Input Array Is Sorted](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/) - Medium
- [4Sum](https://leetcode.com/problems/4sum/) - Medium
- [Subarray Sum Equals K](https://leetcode.com/problems/subarray-sum-equals-k/) - Medium

---

## Tags and Properties
- #dsa #important #revisit  
- #blind75 #neetcode150 #easy-win  
- [[HashMap]] [[Array]]  
- **Revision Date:** 2026-04-07  
- **Problem Link:** [LeetCode - Two Sum](https://leetcode.com/problems/two-sum/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-09)
- [ ] Day 7 Revision (2026-04-14)
- [ ] Day 15 Revision (2026-04-22)
- [ ] Day 30 Revision (2026-05-07)
