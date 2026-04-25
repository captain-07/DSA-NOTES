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
  - #Amazon #Google #Microsoft #Facebook #Bloomberg #Samsung

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #twopointers [[Two Pointers]]
  - #arrays [[Arrays]]
  - #inplace [[In-place Operations]]

---
## Pattern

Two Pointers (Read/Write Index)

---
## Difficulty

Easy
#easy

---

## ⚡ Key Idea (Core Insight)

Maintain a pointer `j` that tracks the position of the first zero (or the "write" location for the next non-zero element). Iterate through the array; whenever a non-zero element is found, swap it with the element at `j` and increment `j`.

---

## ⚡ Quick Recall (VERY IMPORTANT)

"Active Swap": Use a slow pointer to track the placement of non-zeros. Swap every non-zero you find with the slow pointer.

---

## Approach

### Brute Force
- Create a temporary array, iterate through the original array to pick all non-zero elements, then fill the remaining positions with zeros.
- **Time:** O(N) | **Space:** O(N)

### Better (Two-Pass)
- First pass: Use a `write_idx` to move all non-zero elements to the front of the array.
- Second pass: Fill all indices from `write_idx` to the end of the array with zeros.
- **Time:** O(N) | **Space:** O(1)

### Optimal (One-Pass)
- Use two pointers: `i` (current explorer) and `j` (last non-zero boundary).
- When `nums[i] != 0`, swap `nums[i]` with `nums[j]` and increment `j`.
- This ensures all non-zeros are shifted left and zeros are naturally "pushed" to the right in a single traversal.
- **Time:** O(N) | **Space:** O(1)

---

## Code (Python)

```python
class Solution:
    def moveZeroes(self, nums: list[int]) -> None:
        """
        Do not return anything, modify nums in-place instead.
        """
        # j points to the next position to be filled by a non-zero element
        j = 0
        
        for i in range(len(nums)):
            # If current element is non-zero
            if nums[i] != 0:
                # Swap elements at i and j
                nums[i], nums[j] = nums[j], nums[i]
                # Increment the non-zero boundary
                j += 1
```

---

## Dry Run (Smart Example)

Input: `nums = [0, 1, 0, 3, 12]`

| Step | i (Explorer) | j (Boundary) | nums State | Explanation |
| :--- | :--- | :--- | :--- | :--- |
| 1 | 0 | 0 | `[0, 1, 0, 3, 12]` | `nums[0]` is 0, skip. |
| 2 | 1 | 0 | `[1, 0, 0, 3, 12]` | `nums[1]` (1) != 0, swap with `nums[j]`. `j++`. |
| 3 | 2 | 1 | `[1, 0, 0, 3, 12]` | `nums[2]` is 0, skip. |
| 4 | 3 | 1 | `[1, 3, 0, 0, 12]` | `nums[3]` (3) != 0, swap with `nums[j]`. `j++`. |
| 5 | 4 | 2 | `[1, 3, 12, 0, 0]` | `nums[4]` (12) != 0, swap with `nums[j]`. `j++`. |

---

## Edge Cases

- **All Zeros:** `[0, 0, 0]` → `j` stays at 0, no effective swaps occur.
- **No Zeros:** `[1, 2, 3]` → `i` and `j` move together, swapping element with itself.
- **Already Sorted:** `[1, 2, 0, 0]` → Correctly maintains order.
- **Single Element:** `[0]` or `[1]` → Handled by loop range.

---

## Mistakes

- **User Mistake:** No specific note provided.
- **Relative Order:** Forgetting that non-zero elements must maintain their original relative order (avoid sorting).
- **In-place:** Using an extra array when the problem specifically asks for O(1) space.
- **Efficiency:** Using two separate loops (Better approach) when one loop (Optimal swap) is possible.

---

## Complexity

- **Time:** O(N) → Single traversal of the array.
- **Space:** O(1) → Modifying the input array in-place without extra data structures.

---

## Similar Problems

- [Remove Element](https://leetcode.com/problems/remove-element/) - Easy
- [Remove Duplicates from Sorted Array](https://leetcode.com/problems/remove-duplicates-from-sorted-array/) - Easy
- [Apply Operations to an Array](https://leetcode.com/problems/apply-operations-to-an-array/) - Easy
- [Sort Colors](https://leetcode.com/problems/sort-colors/) - Medium

---

## Tags and Properties
- #dsa #important #revisit
- #arrays [[Arrays]]
- #twopointers [[Two Pointers]]
- **Revision Date:** 2026-04-25
- **Problem Link:** [LeetCode - Move Zeroes](https://leetcode.com/problems/move-zeroes/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-27)
- [ ] Day 7 Revision (2026-05-02)
- [ ] Day 15 Revision (2026-05-10)
- [ ] Day 30 Revision (2026-05-25)
