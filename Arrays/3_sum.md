---
created: 2026-03-22
revisions:
  - 2026-03-24
  - 2026-03-29
  - 2026-04-06
  - 2026-04-21
---

# 3 sum
---

## Metadata & Placement Tags
- **Target Companies:** #Amazon #Google #Meta #Microsoft #TCS #Adobe
- **Confidence Level:** [ ] Low [ ] Mid [ ] High
- **Concepts:** #twopointers [[Two Pointers]], #sorting [[Sorting]], #arrays [[Arrays]], #hashmap [[HashMap]]

---

## Difficulty
**Medium**
#medium

---

## Pattern
**Two Pointers (Post-Sorting Strategy)**

---

## Key Idea
The core intuition is to transform the 3-sum problem into a series of 2-sum problems. By sorting the array, we can fix one element ($i$) and use two pointers ($left$ and $right$) to find the remaining two elements such that their sum equals $-nums[i]$. Sorting allows us to efficiently skip duplicate values to ensure every triplet in the result is unique.

---

## Approach

### Brute Force
The naive approach involves three nested loops to check every possible combination of triplets $(i, j, k)$. For each triplet, we check if $nums[i] + nums[j] + nums[k] == 0$. To handle duplicates, we would need to store the triplets in a hash set.
- **Why it's inefficient:** The time complexity is $O(n^3)$, which is too slow for large inputs (typically $n > 500$).

### Optimal
1. **Sort the array:** This is the prerequisite for the two-pointer approach and duplicate handling.
2. **Iterate through the array:** Use a loop with index $i$ from $0$ to $n-3$.
    - If $nums[i] > 0$, break the loop (since the array is sorted, no three positive numbers can sum to zero).
    - **Handle Duplicates:** If $i > 0$ and $nums[i] == nums[i-1]$, skip this iteration.
3. **Two-Pointer Search:** Initialize `left = i + 1` and `right = n - 1`.
    - Calculate `current_sum = nums[i] + nums[left] + nums[right]`.
    - If `current_sum == 0`:
        - Add `[nums[i], nums[left], nums[right]]` to the result.
        - Move `left` forward and `right` backward.
        - **Skip Duplicates:** Increment `left` while $nums[left] == nums[left-1]$ and decrement `right` while $nums[right] == nums[right+1]$.
    - If `current_sum < 0`: Increment `left` to increase the sum.
    - If `current_sum > 0`: Decrement `right` to decrease the sum.

---

## Code

```python
def threeSum(nums):
    res = []
    nums.sort() # Sort to enable two-pointer and duplicate skipping
    
    for i in range(len(nums)):
        # If the first number is > 0, no triplet can sum to 0
        if nums[i] > 0:
            break
            
        # Mistake check: Skip duplicate elements for the first position
        if i > 0 and nums[i] == nums[i - 1]:
            continue
            
        left, right = i + 1, len(nums) - 1
        while left < right:
            three_sum = nums[i] + nums[left] + nums[right]
            
            if three_sum > 0:
                right -= 1
            elif three_sum < 0:
                left += 1
            else:
                res.append([nums[i], nums[left], nums[right]])
                left += 1
                right -= 1
                
                # Skip duplicate elements for the second and third positions
                while left < right and nums[left] == nums[left - 1]:
                    left += 1
                while left < right and nums[right] == nums[right + 1]:
                    right -= 1
                    
    return res
```

---

## Dry Run
**Input:** `nums = [-1, 0, 1, 2, -1, -4]`
**Sorted:** `[-4, -1, -1, 0, 1, 2]`

| Step | `i` (value) | `left` (value) | `right` (value) | `current_sum` | Action | `ans` |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | 0 (-4) | 1 (-1) | 5 (2) | -3 | `left++` | `[]` |
| 2 | 1 (-1) | 2 (-1) | 5 (2) | 0 | **Found**, `L++, R--` | `[[-1, -1, 2]]` |
| 3 | 1 (-1) | 3 (0) | 4 (1) | 0 | **Found**, `L++, R--` | `[[-1, -1, 2], [-1, 0, 1]]` |
| 4 | 2 (-1) | - | - | - | Skip (Duplicate) | `[[-1, -1, 2], [-1, 0, 1]]` |

---

## Edge Cases
1. **Empty Array or $n < 3$:** Should return an empty list `[]`.
2. **All Zeros:** `[0, 0, 0, 0]` should return `[[0, 0, 0]]` (only one unique triplet).
3. **No Triplets:** `[1, 2, -2, -1]` should return `[]`.
4. **All Positive/Negative:** If all elements are $>0$ or all are $<0$, return `[]`.

---

## Mistakes

> [!CAUTION] Mistakes
> - **Ignoring Duplicates:** Failing to check `nums[i] == nums[i-1]` results in redundant triplets. As requested: **Always check with previous elements for repetition.**
> - **Missing the Sorted Condition:** Forgetting to sort `nums` at the start breaks the two-pointer logic and the duplicate skipping mechanism.
> - **Incorrect Pointer Update:** Moving only one pointer when a sum of zero is found. You must move both `left` and `right` and then skip their respective duplicates to avoid infinite loops or duplicates.
> - **Overflow (in other languages):** In C++ or Java, be wary of large integer sums, though less common in 3-sum than 4-sum.

---

## Complexity
- **Time Complexity:** $O(n^2)$
  - Sorting takes $O(n \log n)$. The outer loop runs $n$ times, and the inner two-pointer scan takes $O(n)$ in the worst case, leading to $O(n^2)$ overall.
- **Space Complexity:** $O(1)$ or $O(n)$
  - Excluding the space for the output, space complexity depends on the sorting algorithm's implementation (e.g., $O(n)$ for Python's Timsort or $O(1)$ for HeapSort).

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-03-24)
- [ ] Day 7 Revision (2026-03-29)
- [ ] Day 15 Revision (2026-04-06)
- [ ] Day 30 Revision (2026-04-21)
