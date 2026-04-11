---
created: 2026-04-10
revisions:
  - 2026-04-12
  - 2026-04-17
  - 2026-04-25
  - 2026-05-10
---

Here is a comprehensive, structured Obsidian note for the **Two Sum** problem.

---

# 🧠 Two Sum

---
### 📋 Metadata
- **Date:** 2026-04-10
- **Difficulty:** 🏆 Easy
- **Pattern:** 🏗️ Hash Map
- **Source:** [LeetCode 1](https://leetcode.com/problems/two-sum/)
- **Tags:** #dsa #hash-map #leetcode #arrays

---

## 🧩 Key Idea
Use a **Hash Map** to store the value and index of previously seen numbers, allowing us to check for the "complement" ($target - current$) in constant $O(1)$ time.

---

## 🚀 Approach
1. **Initialize** an empty hash map (dictionary) where keys are the numbers from the array and values are their indices.
2. **Iterate** through the array using index `i` and value `num`.
3. **Calculate the Complement**: `complement = target - num`.
4. **Check the Map**:
   - If `complement` exists in the map, it means we found the two numbers that sum to the target. Return their indices: `[map[complement], i]`.
   - If `complement` does not exist, add the current number and its index to the map: `map[num] = i`.
5. **Why this works**: By storing visited numbers, we effectively "look back" at every step to see if the missing piece of our puzzle has already been encountered.

---

## 💻 Code
```python
def twoSum(nums: list[int], target: int) -> list[int]:
    # hash_map stores {value: index}
    prev_map = {} 
    
    for i, n in enumerate(nums):
        diff = target - n
        
        # If the complement is found, return the pair of indices
        if diff in prev_map:
            return [prev_map[diff], i]
        
        # Otherwise, store the current number and its index
        prev_map[n] = i
        
    return [] # Should not be reached based on problem constraints
```

---

## 🏗️ Pattern
> [!TIP]
> **Hash Map (Look-up Optimization)**
> This pattern is used whenever you need to find a relationship between elements in an array (like pairs, triplets, or frequencies) in a single pass instead of nested loops.

---

## 🏃 Dry Run
**Input:** `nums = [2, 7, 11, 15]`, `target = 9`

| Index (`i`) | Num (`n`) | Complement (`9-n`) | In Map? | Action | Map State |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 0 | 2 | 7 | No | Add 2 | `{2: 0}` |
| 1 | 7 | 2 | **Yes!** | Return `[0, 1]` | - |

---

## ⚠️ Edge Cases
- **Negative Numbers:** Works fine (e.g., `[-3, 4, 3, 90]`, target `0`).
- **Large Targets:** Limited only by integer size.
- **Duplicate Numbers:** If `nums = [3, 3]` and `target = 6`, the first `3` is stored, and the second `3` finds the first one in the map.
- **No Solution:** The problem typically guarantees one, but returning an empty list is the standard fallback.

---

## 💡 Mistakes
> [!WARNING]
> **User Note:** No specific note provided.
> 
> **Common Pitfall to Avoid:** 
> - **Using the same element twice:** Ensure you check the map *before* adding the current element to the map, or ensure the indices are different. 
> - **Sorting First:** Don't sort the array if you need to return original indices, as sorting changes the positions. If you do sort, you must use a Two-Pointer approach with a copy of original indices.

---

## 📊 Complexity
- **Time Complexity:** $O(n)$ — We traverse the list containing $n$ elements only once. Each look-up in the hash table costs $O(1)$ on average.
- **Space Complexity:** $O(n)$ — In the worst case, we store every element of the array in the hash map.

---

## 🔗 Similar Problems
- [ ] [3Sum](https://leetcode.com/problems/3sum/) (Medium)
- [ ] [Two Sum II - Input Array Is Sorted](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/) (Medium)
- [ ] [Subarray Sum Equals K](https://leetcode.com/problems/subarray-sum-equals-k/) (Medium)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-12)
- [ ] Day 7 Revision (2026-04-17)
- [ ] Day 15 Revision (2026-04-25)
- [ ] Day 30 Revision (2026-05-10)
