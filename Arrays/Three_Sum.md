---
created: 2026-03-22
revisions:
  - 2026-03-24
  - 2026-03-29
  - 2026-04-06
  - 2026-04-21
---

# Three Sum
---

## Difficulty
Medium
#medium

---

## Pattern
**Two Pointers** & **Sorting**

---

## Key Idea
The core intuition is to sort the array first, then iterate through each element as a potential first member of a triplet. For each selected element, use a two-pointer approach on the remaining subarray to find pairs that sum to the negative of the selected element, effectively reducing the problem to multiple "Two Sum II" instances.

---

## Approach

### Brute Force
The naive solution involves using three nested loops to check every possible combination of three integers $(i, j, k)$. For each triplet, we verify if $nums[i] + nums[j] + nums[k] == 0$. To avoid returning duplicate triplets, we would need to store results in a set and sort each triplet before insertion.
- **Time Complexity:** $O(n^3)$ due to the three nested loops.
- **Inefficiency:** This approach performs many redundant calculations and is far too slow for arrays larger than a few hundred elements.

### Optimal
The optimal approach leverages the properties of a sorted array to navigate the search space efficiently.
1.  **Sort:** Sort the input array in ascending order.
2.  **Fix One Element:** Iterate through the array with index `i`. If `nums[i]` is the same as `nums[i-1]`, skip it to prevent duplicate triplets.
3.  **Two Pointers:** For the current `nums[i]`, initialize `left = i + 1` and `right = len(nums) - 1`.
4.  **Convergence:** 
    - If `nums[i] + nums[left] + nums[right] == 0`, record the triplet.
    - To avoid duplicates, increment `left` and decrement `right` until they point to different values.
    - If the sum is less than zero, increment `left` to increase the sum.
    - If the sum is greater than zero, decrement `right` to decrease the sum.

---

## Code
```python
def threeSum(nums):
    res = []
    # Sort is mandatory to use the two-pointer logic and handle duplicates
    nums.sort() 
    
    for i in range(len(nums)):
        # If the current number is > 0, no triplet can sum to 0 anymore
        if nums[i] > 0:
            break
            
        # Skip the same element to avoid duplicate triplets in the result
        if i > 0 and nums[i] == nums[i-1]:
            continue
            
        left, right = i + 1, len(nums) - 1
        
        while left < right:
            current_sum = nums[i] + nums[left] + nums[right]
            
            if current_sum == 0:
                res.append([nums[i], nums[left], nums[right]])
                
                # Move pointers and skip duplicates for the 'left' and 'right' values
                while left < right and nums[left] == nums[left + 1]:
                    left += 1
                while left < right and nums[right] == nums[right - 1]:
                    right -= 1
                    
                left += 1
                right -= 1
            elif current_sum < 0:
                # Sum is too small, move left pointer to a larger value
                left += 1
            else:
                # Sum is too large, move right pointer to a smaller value
                right -= 1
                
    return res
```

---

## Dry Run
**Input:** `nums = [-1, 0, 1, 2, -1, -4]`  
**Sorted:** `[-4, -1, -1, 0, 1, 2]`

| Step | i | nums[i] | left | right | nums[left] | nums[right] | Sum | Action | Result |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | 0 | -4 | 1 | 5 | -1 | 2 | -3 | Sum < 0, left++ | `[]` |
| 2 | 1 | -1 | 2 | 5 | -1 | 2 | 0 | **Match!**, Move both | `[[-1,-1,2]]` |
| 3 | 1 | -1 | 3 | 4 | 0 | 1 | 0 | **Match!**, Move both | `[[-1,-1,2], [-1,0,1]]` |
| 4 | 2 | -1 | - | - | - | - | - | Skip (Duplicate) | - |
| 5 | 3 | 0 | 4 | 5 | 1 | 2 | 3 | Sum > 0, right-- | Final Result |

---

## Edge Cases
1.  **Array length < 3:** Should immediately return an empty list `[]`.
2.  **All Zeros:** `[0, 0, 0, 0]` should correctly return `[[0, 0, 0]]` only once.
3.  **No Solution:** An array like `[1, 2, 3]` where all elements are positive.
4.  **Highly Duplicated:** `[-2, -2, -2, 0, 2, 2, 2]` requires robust duplicate skipping logic.
5.  **Empty Array:** Handled by the loop range; returns `[]`.

---

## Mistakes
> [!CAUTION] Mistakes
> - **Ignoring the Sort:** The most critical mistake is trying to use two pointers on an unsorted array; it will not work because there is no directional logic for the sum.
> - **Duplicate Results:** Forgetting to skip duplicates for the `i` index AND the `left`/`right` pointers leads to repetitive triplets in the output.
> - **User Note:** As specified, you must **use two pointers after sorting**. This is the standard optimization that brings the complexity down from cubic to quadratic.
> - **Condition for Breaking:** Some forget that if `nums[i] > 0`, since the array is sorted, no combination of `nums[i]` and subsequent numbers can ever sum to zero.

---

## Complexity
- **Time Complexity:** $O(n^2)$  
  Sorting the array takes $O(n \log n)$, and the main loop combined with the two-pointer search takes $O(n^2)$ time.
- **Space Complexity:** $O(1)$ or $O(n)$  
  Excluding the output list, the space complexity depends on the sorting implementation (Python's Timsort uses $O(n)$ auxiliary space).

---

## Metadata & Placement Tags
#Amazon #Google #Meta #Microsoft #Adobe #TCS #Service-Based  
**Confidence Level:** [ ] Low [ ] Mid [x] High

#twopointers [[Two Pointers]]
#sorting [[Sorting]]
#arrays [[Arrays]]
#duplicatehandling [[Duplicate Handling]]

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-03-24)
- [ ] Day 7 Revision (2026-03-29)
- [ ] Day 15 Revision (2026-04-06)
- [ ] Day 30 Revision (2026-04-21)
