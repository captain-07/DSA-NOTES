---
created: 2026-04-10
revisions:
  - 2026-04-12
  - 2026-04-17
  - 2026-04-25
  - 2026-05-10
---

---
title: Two Sum
difficulty: Easy
pattern: Hashing
leetcode_url: https://leetcode.com/problems/two-sum/
tags: [dsa, hashing, leetcode]
---

# 1. Two Sum

## 🧩 Key Idea
Use a **Hash Map** to store the numbers we've seen so far and their indices, allowing us to find the "complement" ($target - current\_value$) in constant time.

## 🚀 Approach
Instead of checking every possible pair (which takes $O(n^2)$), we can solve this in a single pass:
1. Initialize an empty hash map `prevMap` (Value -> Index).
2. Iterate through the array `nums` with index `i`.
3. Calculate the `diff = target - nums[i]`.
4. **Check:** If `diff` exists in `prevMap`, we've found our pair! Return `[prevMap[diff], i]`.
5. **Update:** If not, add the current number and its index to the map: `prevMap[nums[i]] = i`.

> [!TIP]
> This works because for every $x$, we are looking for $y$ such that $x + y = target$. By the time we reach $y$, $x$ is already waiting in our map.

## 💻 Code
```python
def twoSum(nums: list[int], target: int) -> list[int]:
    # val -> index
    prevMap = {} 
    
    for i, n in enumerate(nums):
        diff = target - n
        if diff in prevMap:
            return [prevMap[diff], i]
        prevMap[n] = i
    return []
```

## 🏗️ Pattern
**Hashing / Complement Lookup**: This pattern is useful whenever you need to find a pair or check for the existence of an element relative to the current one.

## 🏃 Dry Run
**Input:** `nums = [2, 11, 7, 15]`, `target = 9`

| Step | `n` | `diff` (9 - `n`) | In `prevMap`? | `prevMap` State (After) |
| :--- | :--- | :--- | :--- | :--- |
| 1 | 2 | 7 | No | `{2: 0}` |
| 2 | 11 | -2 | No | `{2: 0, 11: 1}` |
| 3 | 7 | 2 | **Yes!** (at index 0) | **Return [0, 2]** |

## ⚠️ Edge Cases
- **Negative Numbers:** Works fine (e.g., `[-1, -2, -3], target = -5`).
- **Same Value Used Twice:** If `nums = [3, 3], target = 6`, the first `3` is stored, and the second `3` finds it.
- **Large Inputs:** The $O(n)$ approach scales well, whereas $O(n^2)$ would TLE (Time Limit Exceeded).

## 💡 Mistakes
*Since no specific mistake was provided, here are common pitfalls:*
- **Using the same element twice:** Ensure you don't return the same index (e.g., if `target = 6` and `nums = [3]`, don't return `[0, 0]`). The hash map approach naturally avoids this by checking the map *before* adding the current element.
- **Sorting First:** While sorting allows a two-pointer approach, it takes $O(n \log n)$ and loses the original indices, requiring extra work to track them.

## 📊 Complexity
- **Time Complexity:** $O(n)$ — We traverse the list once. Each lookup in the hash map is $O(1)$ on average.
- **Space Complexity:** $O(n)$ — In the worst case, we store almost all elements in the hash map.

## 🏆 Difficulty
**Easy**

## 📎 Metadata & Placement Tags
#dsa #hashing #leetcode #arrays

## 🔗 Similar Problems
- [[3Sum]] (Medium - Two Pointer / Hashing extension)
- [[Two Sum II - Input Array Is Sorted]] (Medium - Two Pointer optimized)
- [[Subarray Sum Equals K]] (Medium - Prefix Sum + Hashing)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-12)
- [ ] Day 7 Revision (2026-04-17)
- [ ] Day 15 Revision (2026-04-25)
- [ ] Day 30 Revision (2026-05-10)
