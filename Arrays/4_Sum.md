---
created: 2026-04-25
revisions:
  - 2026-04-27
  - 2026-05-02
  - 2026-05-10
  - 2026-05-25
---

# 4 Sum

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Meta #Google #Microsoft #Apple #Adobe

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #sorting [[Sorting]], #twopointers [[Two Pointers]], #array [[Array]]

## Pattern

Two Pointers + Sorting (Reduced from $O(N^4)$ to $O(N^3)$)

---
## Difficulty

Medium  
#medium

---

## ⚡ Key Idea (Core Insight)

The problem is an extension of **3 Sum**. Sort the array, fix two elements using nested loops ($i$ and $j$), and then use the **Two-Pointer** technique ($left$ and $right$) to find the remaining two elements that sum to the target.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Sort $\to$ Nested loops for $i$ and $j$ $\to$ Skip duplicates for $i, j, left, right$ $\to$ Standard two-pointer logic for the inner pair.

---

## Approach

### Brute Force
- Four nested loops to check every possible quadruplet.
- **Time Complexity:** $O(N^4)$

### Better
- Three nested loops and a **HashSet** to store the fourth required value ($target - (a+b+c)$).
- **Time Complexity:** $O(N^3)$
- **Space Complexity:** $O(N)$ for the set.

### Optimal
1. **Sort** the array.
2. Fix $i$ from $0$ to $n-1$. Skip if $nums[i] == nums[i-1]$.
3. Fix $j$ from $i+1$ to $n-1$. Skip if $nums[j] == nums[j-1]$.
4. Initialize $left = j+1$ and $right = n-1$.
5. While $left < right$:
   - If $sum == target$: add to result, move both pointers, and **skip duplicates**.
   - If $sum < target$: $left++$.
   - If $sum > target$: $right--$.

---

## Code (Python)

```python
class Solution:
    def fourSum(self, nums: list[int], target: int) -> list[list[int]]:
        nums.sort()
        n = len(nums)
        res = []
        
        for i in range(n):
            # Skip duplicates for i
            if i > 0 and nums[i] == nums[i-1]:
                continue
            
            for j in range(i + 1, n):
                # Skip duplicates for j
                if j > i + 1 and nums[j] == nums[j-1]:
                    continue
                
                # Two pointers
                left, right = j + 1, n - 1
                while left < right:
                    curr_sum = nums[i] + nums[j] + nums[left] + nums[right]
                    
                    if curr_sum == target:
                        res.append([nums[i], nums[j], nums[left], nums[right]])
                        left += 1
                        right -= 1
                        # Skip duplicates for left and right
                        while left < right and nums[left] == nums[left-1]:
                            left += 1
                        while left < right and nums[right] == nums[right+1]:
                            right -= 1
                    elif curr_sum < target:
                        left += 1
                    else:
                        right -= 1
        return res
```

---

## Dry Run (Smart Example)

**Input:** `nums = [1, 0, -1, 0, -2, 2]`, `target = 0`  
**Sorted:** `[-2, -1, 0, 0, 1, 2]`

| Step | i, j (Indices) | left, right | Sum Calculation | Action |
| :--- | :--- | :--- | :--- | :--- |
| 1 | i=0 (-2), j=1 (-1) | L=2 (0), R=5 (2) | -2-1+0+2 = -1 | Sum < Target, L++ |
| 2 | i=0 (-2), j=1 (-1) | L=3 (0), R=5 (2) | -2-1+0+2 = -1 | Sum < Target, L++ |
| 3 | i=0 (-2), j=2 (0) | L=3 (0), R=5 (2) | -2+0+0+2 = 0 | **Match!** [-2, 0, 0, 2] |
| 4 | i=1 (-1), j=2 (0) | L=3 (0), R=4 (1) | -1+0+0+1 = 0 | **Match!** [-1, 0, 0, 1] |

---

## Edge Cases

- `len(nums) < 4`: Return empty list immediately.
- `All elements same`: If $4 \times nums[0] == target$, return one quadruplet; else empty.
- `Target is very large/small`: Integer overflow risk in some languages (not Python).
- `No possible sum`: Ensure the pointers exhaust correctly without error.

---

## Mistakes

- **User Mistake:** No specific note provided (Initial lack of structured documentation).
- Forgetting to sort the array before using two pointers.
- Not skipping duplicates for $i$ and $j$, leading to redundant quadruplets.
- Only skipping duplicates for $left$ or $right$, but not both after a match.

---

## Complexity

- **Time:** $O(N^3)$ → Two nested loops $O(N^2)$ multiplied by two-pointer scan $O(N)$.
- **Space:** $O(1)$ or $O(N)$ → Depending on the sorting algorithm implementation and output storage.

---

## Similar Problems

- [Two Sum](https://leetcode.com/problems/two-sum/) - Easy
- [3Sum](https://leetcode.com/problems/3sum/) - Medium
- [3Sum Closest](https://leetcode.com/problems/3sum-closest/) - Medium
- [4Sum II](https://leetcode.com/problems/4sum-ii/) - Medium

---

## Tags and Properties
- #dsa #important #revisit #arrays #algorithms
- [[Two Pointers]] [[Sorting]]
- **Revision Date:** 2026-04-25
- **Problem Link:** [LeetCode 4Sum](https://leetcode.com/problems/4sum/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-27)
- [ ] Day 7 Revision (2026-05-02)
- [ ] Day 15 Revision (2026-05-10)
- [ ] Day 30 Revision (2026-05-25)
