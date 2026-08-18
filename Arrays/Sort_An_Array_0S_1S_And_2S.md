---
created: 2026-04-25
revisions:
  - 2026-04-27
  - 2026-05-02
  - 2026-05-10
  - 2026-05-25
---

# Sort An Array Of 0s 1s And 2s

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Microsoft #Adobe #Walmart #Flipkart #Google

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #arrays [[Arrays]]
  - #twopointers [[Two Pointers]]
  - #sorting [[Sorting]]

---
## Pattern

Three-way Partitioning (Dutch National Flag Algorithm)

---
## Difficulty

Medium  
#medium

---

## ⚡ Key Idea (Core Insight)

Use three pointers (`low`, `mid`, `high`) to maintain three boundaries: 
1. `[0...low-1]` contains only 0s.
2. `[low...mid-1]` contains only 1s.
3. `[high+1...n-1]` contains only 2s.
The `mid` pointer explores the unknown region `[mid...high]`.

---

## ⚡ Quick Recall (VERY IMPORTANT)

- **If 0:** Swap `nums[low]` and `nums[mid]`, increment both.
- **If 1:** Just increment `mid`.
- **If 2:** Swap `nums[mid]` and `nums[high]`, decrement `high` (**Don't** move `mid`).

---

## Approach

### Brute Force
- Sort the array using any standard sorting algorithm (e.g., Merge Sort or Quick Sort).
- Time: O(N log N), Space: O(1) or O(N) depending on sort.

### Better
- **Counting Sort (Two Pass):** Count occurrences of 0, 1, and 2. Overwrite the original array.
- Time: O(2N) ≈ O(N), Space: O(1).

### Optimal
- **Dutch National Flag (One Pass):** Process each element once using three pointers to place 0s at the start and 2s at the end.
- Time: O(N), Space: O(1).

---

## Code (Python)

```python
class Solution:
    def sortColors(self, nums: list[int]) -> None:
        """
        Do not return anything, modify nums in-place instead.
        """
        low = 0
        mid = 0
        high = len(nums) - 1
        
        while mid <= high:
            if nums[mid] == 0:
                # Swap with low pointer, increment both
                nums[low], nums[mid] = nums[mid], nums[low]
                low += 1
                mid += 1
            elif nums[mid] == 1:
                # 1 is in the correct middle section, just move forward
                mid += 1
            else: # nums[mid] == 2
                # Swap with high pointer, only decrement high
                # We don't increment mid because the swapped value is unknown
                nums[mid], nums[high] = nums[high], nums[mid]
                high -= 1
```

---

## Dry Run (Smart Example)

Input: `nums = [2, 0, 1]`

| Step | Pointers (L, M, H) | nums[mid] | Action | Array State |
| :--- | :--- | :--- | :--- | :--- |
| 1 | L=0, M=0, H=2 | 2 | Swap(M, H), H-- | [1, 0, 2] |
| 2 | L=0, M=0, H=1 | 1 | M++ | [1, 0, 2] |
| 3 | L=0, M=1, H=1 | 0 | Swap(L, M), L++, M++ | [0, 1, 2] |
| 4 | L=1, M=2, H=1 | - | Loop Ends (M > H) | [0, 1, 2] |

---

## Edge Cases

- **Empty Array:** `[]` handled by loop condition.
- **All Identical:** `[1, 1, 1]` or `[0, 0, 0]` - pointers traverse correctly.
- **Only Two Colors:** `[0, 2, 0, 2]` - algorithm naturally partitions.
- **Already Sorted:** `[0, 1, 2]` - `mid` moves through with no swaps.

---

## Mistakes

- **Mid Increment on 2:** Forgetting that after swapping `nums[mid]` with `nums[high]`, the new `nums[mid]` is unexamined and could be a 0.
- **Loop Condition:** Using `mid < high` instead of `mid <= high` (misses the last element).
- **User Mistake:** No specific note provided (ensure full structure is memorized).

---

## Complexity

Time: O(N) → Single pass through the array.  
Space: O(1) → In-place swaps only.

---

## Similar Problems

- [Sort Colors](https://leetcode.com/problems/sort-colors/) - Medium
- [Move Zeroes](https://leetcode.com/problems/move-zeroes/) - Easy
- [Sort Array By Parity](https://leetcode.com/problems/sort-array-by-parity/) - Easy
- [3-Way Partitioning](https://www.geeksforgeeks.org/three-way-partitioning-of-an-array-around-a-given-range/) - Medium

---

## Tags and Properties
  - #dsa #important #revisit  
  - #arrays #twopointers #partitioning
  - [[Two Pointers]] [[Dutch National Flag]]
  - **Revision Date:** 2026-04-25
  - **Problem Link:** [LeetCode - Sort Colors](https://leetcode.com/problems/sort-colors/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-27)
- [ ] Day 7 Revision (2026-05-02)
- [ ] Day 15 Revision (2026-05-10)
- [ ] Day 30 Revision (2026-05-25)
