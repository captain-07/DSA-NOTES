# 4 Sum
---
**Placement Prep:** #Amazon #Google #Microsoft #Meta #Service-Based
**Confidence Level:** [ ] Low [ ] Mid [ ] High

---
## Pattern
**Two Pointers (on a sorted array)**. This problem is an extension of the classic "3 Sum" problem, which itself builds upon the "2 Sum" pattern. By fixing two elements, the problem is reduced to finding the remaining two elements, which is a perfect use case for the two-pointers technique.

---
## Logic Evolution
- **Brute Force:** The most straightforward approach is to use four nested loops to iterate through every possible combination of four elements in the array. For each combination, you sum the elements and check if they equal the target. This is highly inefficient due to its $O(n^4)$ time complexity and is not feasible for large inputs.

- **Better:** An improvement is to use three nested loops to fix the first three numbers (`a`, `b`, `c`). Then, the problem becomes finding a fourth number `d` such that `d = target - (a + b + c)`. We can store all array elements in a hash set for $O(1)$ lookups. This brings the time complexity down to $O(n^3)$.

- **Optimal:** The most efficient approach sorts the array first. Then, it iterates through the array with two nested loops, fixing the first (`i`) and second (`j`) numbers. For the remaining portion of the array, it applies the **Two Pointers** pattern. A `left` pointer starts at `j + 1` and a `right` pointer starts at the end of the array. These two pointers converge, calculating the sum and adjusting their positions based on whether the sum is less than, greater than, or equal to the remaining target. Crucially, this approach requires careful handling to skip duplicate values and avoid redundant quadruplets in the output.

---
## Python Implementation (Optimal)
```python
def fourSum(nums: list[int], target: int) -> list[list[int]]:
    """
    Finds all unique quadruplets in the array which give the sum of target.
    """
    nums.sort()
    n = len(nums)
    ans = []

    # Outer loop for the first element
    for i in range(n - 3):
        # Skip duplicates for the first element.
        # Compare with the previous element to ensure we process each number once.
        if i > 0 and nums[i] == nums[i - 1]:
            continue

        # Second loop for the second element
        for j in range(i + 1, n - 2):
            # Skip duplicates for the second element.
            # Compare with the previous element in this sub-problem.
            if j > i + 1 and nums[j] == nums[j - 1]:
                continue

            # Two-pointer approach for the remaining two elements
            left, right = j + 1, n - 1
            while left < right:
                current_sum = nums[i] + nums[j] + nums[left] + nums[right]

                if current_sum < target:
                    left += 1
                elif current_sum > target:
                    right -= 1
                else:
                    # Found a valid quadruplet
                    ans.append([nums[i], nums[j], nums[left], nums[right]])
                    
                    # Skip all duplicates for the third element (left pointer)
                    while left < right and nums[left] == nums[left + 1]:
                        left += 1
                    
                    # Skip all duplicates for the fourth element (right pointer)
                    while left < right and nums[right] == nums[right - 1]:
                        right -= 1
                    
                    # Move pointers to look for a new, unique pair
                    left += 1
                    right -= 1
    return ans

```

---
## Dry Run Table
**Input:** `nums = [-2, -1, 0, 0, 1, 2]`, `target = 0` (array is pre-sorted)

| `i` (val) | `j` (val) | `left` (val) | `right` (val) | `current_sum` | Action                                                                                | `ans`                  |
| :-------: | :-------: | :----------: | :-----------: | :-----------: | :------------------------------------------------------------------------------------ | :--------------------- |
| 0 (`-2`)  | 1 (`-1`)  |   2 (`0`)    |    5 (`2`)    |     `-1`      | `sum < target`, `left++`                                                              | `[]`                   |
| 0 (`-2`)  | 1 (`-1`)  |   3 (`0`)    |    5 (`2`)    |     `-1`      | `sum < target`, `left++`                                                              | `[]`                   |
| 0 (`-2`)  | 1 (`-1`)  |   4 (`1`)    |    5 (`2`)    |      `0`      | `sum == target`, found `[-2, -1, 1, 2]`. Skip duplicates (none). `left++`, `right--`. | `[[-2, -1, 1, 2]]`     |
| 0 (`-2`)  | 1 (`-1`)  |   5 (`2`)    |    4 (`1`)    |       -       | `left >= right`, inner loop ends.                                                     | `[[-2, -1, 1, 2]]`     |
| 0 (`-2`)  |  2 (`0`)  |   3 (`0`)    |    5 (`2`)    |      `0`      | `sum == target`, found `[-2, 0, 0, 2]`. Skip `left` to index 4. `left++`, `right--`.  | `[..., [-2, 0, 0, 2]]` |
| 0 (`-2`)  |  2 (`0`)  |   5 (`2`)    |    4 (`1`)    |       -       | `left >= right`, inner loop ends.                                                     | `[..., [-2, 0, 0, 2]]` |
| 1 (`-1`)  |  2 (`0`)  |   3 (`0`)    |    4 (`1`)    |      `0`      | `sum == target`, found `[-1, 0, 0, 1]`. Skip `left` to index 4. `left++`, `right--`.  | `[..., [-1, 0, 0, 1]]` |

*... The process continues until all combinations are checked.*

---
## Edge Cases
1.  **Array too small:** If the input array has fewer than 4 elements, no quadruplet is possible. The code should return an empty list.
2.  **No solution found:** If no combination of four numbers sums to the target, the final result should be an empty list.
3.  **All identical elements:** For an input like `nums = [2, 2, 2, 2, 2]` and `target = 8`, the algorithm must correctly identify `[2, 2, 2, 2]` and return it only once.
4.  **Mixed positive and negative integers:** The logic must robustly handle summations that cross zero.

---
## Common Mistakes

> [!CAUTION] Mistakes
> 1.  **Forgetting to Sort:** The Two Pointers approach is entirely dependent on the array being sorted. Skipping this step will produce incorrect results.
> 2.  **Incorrectly Skipping Duplicates:** This is the most frequent "gotcha".
>     -   **Outer Loops (`i`, `j`):** Always check against the *previous* element (e.g., `if i > 0 and nums[i] == nums[i-1]`). If you check against the *next* element (`nums[i] == nums[i+1]`), you will incorrectly skip the first occurrence of a number in a sequence of duplicates, potentially missing a valid solution.
>     -   **Inner Pointers (`left`, `right`):** After finding a valid quadruplet, you **must use a `while` loop**, not an `if` statement, to skip over all subsequent identical elements (e.g., `while left < right and nums[left] == nums[left+1]`). A simple `if` only advances the pointer by one, which will result in duplicate quadruplets being added to your answer.
> 3.  **Off-by-One Errors in Loops:** Ensure loop ranges are correct (e.g., `range(n-3)` for `i`) to avoid `IndexError` and to ensure there are enough elements left for a full quadruplet.

---
## Complexity Analysis
-   **Time Complexity:** $O(n^3)$
    -   The initial sort takes $O(n \log n)$. The nested loops (`i` and `j`) combined with the linear scan of the two pointers (`left` and `right`) results in a cubic time complexity, which dominates the sorting step.
-   **Space Complexity:** $O(1)$ (excluding the output list)
    -   The algorithm uses a fixed amount of extra space for variables. The space required for the answer list is not counted as auxiliary space, but if it were, it would be $O(k)$, where $k$ is the number of valid quadruplets.