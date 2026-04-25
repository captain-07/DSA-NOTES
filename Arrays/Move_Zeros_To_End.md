---
created: 2026-04-25
revisions:
  - 2026-04-27
  - 2026-05-02
  - 2026-05-10
  - 2026-05-25
---

# Move Zeros To End

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Microsoft #Google #Meta #Bloomberg #Apple #Uber

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #array [[Array]]
  - #twopointers [[Two Pointers]]
  - #inplace [[In-place Operations]]

## Pattern

Two Pointers (Read/Write Heads)

---
## Difficulty

Easy
#easy

---

## ⚡ Key Idea (Core Insight)

Maintain a `last_non_zero_index` (the "write" pointer). Iterate through the array; whenever a non-zero element is found, move it to the `last_non_zero_index` and increment that index. This effectively "bubbles" zeros to the end or non-zeros to the front.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Use two pointers: `i` explores the array, `j` tracks the position for the next non-zero element. **Swap** `arr[i]` and `arr[j]` when `arr[i] != 0`.

---

## Approach

### Brute Force
- Create a new array of the same size. Iterate the original array and copy all non-zero elements to the new array. Fill the remaining spots with zeros.
- **Time:** O(N) | **Space:** O(N)

### Optimal (Two Pointer Swap - One Pass)
1. Initialize a pointer `j = 0` to track the position of the next non-zero element.
2. Iterate through the array with pointer `i` from `0` to `n-1`.
3. If `arr[i]` is not zero:
   - Swap `arr[i]` with `arr[j]`.
   - Increment `j`.
4. This ensures all non-zeros are moved forward in their original order, and zeros are naturally pushed back.

---

## Code (Python)

```python
class Solution:
    def moveZeroes(self, nums: list[int]) -> None:
        """
        Do not return anything, modify nums in-place instead.
        """
        # j is the position to place the next non-zero element
        j = 0
        
        for i in range(len(nums)):
            # If current element is non-zero
            if nums[i] != 0:
                # Swap elements at i and j
                # If i == j, no actual change happens
                nums[i], nums[j] = nums[j], nums[i]
                # Move the write pointer forward
                j += 1
```

---

## Dry Run (Smart Example)

**Input:** `nums = [0, 1, 0, 3, 12]`

| Step | `i` | `nums[i]` | Action | `j` (after) | Array State |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | 0 | 0 | `nums[0]` is 0, skip | 0 | `[0, 1, 0, 3, 12]` |
| 2 | 1 | 1 | `nums[1] != 0`, swap `nums[1]` & `nums[0]` | 1 | `[1, 0, 0, 3, 12]` |
| 3 | 2 | 0 | `nums[2]` is 0, skip | 1 | `[1, 0, 0, 3, 12]` |
| 4 | 3 | 3 | `nums[3] != 0`, swap `nums[3]` & `nums[1]` | 2 | `[1, 3, 0, 0, 12]` |
| 5 | 4 | 12 | `nums[4] != 0`, swap `nums[4]` & `nums[2]` | 3 | `[1, 3, 12, 0, 0]` |

---

## Edge Cases

- **All Zeros:** `[0, 0, 0]` -> `j` never moves, array remains same.
- **No Zeros:** `[1, 2, 3]` -> `i` and `j` move together, swapping elements with themselves.
- **Single Element:** `[0]` or `[1]` -> Handled correctly by loop bounds.
- **Zeros already at end:** `[1, 2, 0, 0]` -> No unnecessary swaps of non-zeros after they are placed.

---

## Mistakes

- **Relative Order:** Using a two-pointer approach that swaps from both ends (like QuickSort partition) will break the relative order of non-zero elements.
- **Forgetting the Fill:** If using the "overwrite" method (`nums[j] = nums[i]`), forgetting to fill the remaining indices from `j` to `n-1` with zeros.
- **User Mistake:** No specific note provided. Ensure to verify if the problem requires in-place modification.

---

## Complexity

- **Time:** O(N) → Each element is visited exactly once.
- **Space:** O(1) → No extra data structures used; modification is in-place.

---

## Similar Problems

- [Remove Element](https://leetcode.com/problems/remove-element/) - Easy
- [Remove Duplicates from Sorted Array](https://leetcode.com/problems/remove-duplicates-from-sorted-array/) - Easy
- [Sort Colors](https://leetcode.com/problems/sort-colors/) - Medium
- [Apply Operations to an Array](https://leetcode.com/problems/apply-operations-to-an-array/) - Easy

---

## Tags and Properties
  - #dsa #important #revisit
  - #leetcode283 #arrays #twopointers
  - [[Array]] [[Two Pointers]]
  - **Revision Date:** 2026-04-25
  - **Problem Link:** [LeetCode - Move Zeroes](https://leetcode.com/problems/move-zeroes/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-27)
- [ ] Day 7 Revision (2026-05-02)
- [ ] Day 15 Revision (2026-05-10)
- [ ] Day 30 Revision (2026-05-25)
