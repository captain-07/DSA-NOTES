---
created: 2026-04-25
revisions:
  - 2026-04-27
  - 2026-05-02
  - 2026-05-10
  - 2026-05-25
---

---
# Move Zeros To End

---
### 📊 Metadata
- **Difficulty:** 🟢 Easy
- **Pattern:** #two-pointers
- **Platform:** #leetcode
- **Last Revised:** 2026-04-25

---

## 🧩 Key Idea
The core insight is to use **two pointers** to "bubble" non-zero elements to the front of the array, effectively pushing all zeros to the end while maintaining their relative order.

## 🚀 Approach
We use a two-pointer technique to solve this in a single pass ($O(n)$) without using extra space ($O(1)$).

1.  **Initialize two pointers:**
    -   `j`: Points to the first zero found in the array (or the position where the next non-zero should go).
    -   `i`: Iterates through the array to find non-zero elements.
2.  **Find the first zero:** Before starting the main loop, we can optionally find the index of the first `0`. This becomes the initial position for `j`.
3.  **The Swap Logic:**
    -   Start `i` from `j + 1`.
    -   If `arr[i]` is **not zero**, swap `arr[i]` with `arr[j]`.
    -   Increment `j` after the swap.
    -   Because we only swap when `arr[i]` is non-zero and `arr[j]` is zero, the non-zero elements "collect" at the front.

> [!TIP] 
> This approach is more efficient than "shifting and filling" because swapping moves the zero naturally to the current index of `i`, preparing it for the next swap.

## 💻 Code
```python
def moveZeroes(nums):
    """
    Do not return anything, modify nums in-place instead.
    """
    n = len(nums)
    j = -1
    
    # 1. Find the first zero
    for i in range(n):
        if nums[i] == 0:
            j = i
            break
            
    # 2. If no zero is found, the array is already "done"
    if j == -1:
        return nums
        
    # 3. Two-pointer swap
    for i in range(j + 1, n):
        if nums[i] != 0:
            nums[i], nums[j] = nums[j], nums[i]
            j += 1
            
    return nums
```

## 🏗️ Pattern
**Two Pointers (Slow & Fast):** The slow pointer (`j`) waits at a zero element, while the fast pointer (`i`) searches for the next available non-zero element to bring forward.

## 🏃 Dry Run
**Input:** `[0, 1, 0, 3, 12]`

1.  **Find first zero:** `j = 0` (at index 0).
2.  **Loop starts (i = 1):** `nums[1]` is `1` (Non-Zero).
    - Swap `nums[1]` and `nums[0]`.
    - Array: `[1, 0, 0, 3, 12]`, `j` moves to `1`.
3.  **Loop (i = 2):** `nums[2]` is `0`. Skip.
4.  **Loop (i = 3):** `nums[3]` is `3` (Non-Zero).
    - Swap `nums[3]` and `nums[1]`.
    - Array: `[1, 3, 0, 0, 12]`, `j` moves to `2`.
5.  **Loop (i = 4):** `nums[4]` is `12` (Non-Zero).
    - Swap `nums[4]` and `nums[2]`.
    - Array: `[1, 3, 12, 0, 0]`, `j` moves to `3`.
**Result:** `[1, 3, 12, 0, 0]`

## ⚠️ Edge Cases
- **All Zeros:** `[0, 0, 0]` → Loop finds first zero, but no subsequent non-zeroes to swap.
- **No Zeros:** `[1, 2, 3]` → `j` remains `-1`, function returns early.
- **Single Element:** `[0]` or `[1]` → Handled correctly by loop boundaries.
- **Already Correct:** `[1, 2, 0, 0]` → Handled correctly.

## 💡 Mistakes
> [!WARNING] **Common Pitfall**
> A common mistake is using a second array to store non-zeroes and then filling the rest with zeroes. While this works ($O(n)$ time), it uses **$O(n)$ space**, which usually fails the "In-Place" constraint of this problem.
> 
> **Another mistake:** Forgetting to maintain the **relative order** of non-zero elements. Sorting the array would move zeros to the end (or start) but would destroy the original sequence.

## 📊 Complexity
- **Time Complexity:** $O(n)$ — We traverse the array at most twice (once to find the first zero, once to swap).
- **Space Complexity:** $O(1)$ — No extra data structures are used.

## 🏆 Difficulty
**Easy**

## 📎 Metadata & Placement Tags
#dsa #two-pointers #leetcode #arrays #top-interview-questions

## 🔗 Similar Problems
- [Remove Element](https://leetcode.com/problems/remove-element/)
- [Remove Duplicates from Sorted Array](https://leetcode.com/problems/remove-duplicates-from-sorted-array/)
- [Apply Operations to an Array](https://leetcode.com/problems/apply-operations-to-an-array/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-27)
- [ ] Day 7 Revision (2026-05-02)
- [ ] Day 15 Revision (2026-05-10)
- [ ] Day 30 Revision (2026-05-25)
