---
created: 2026-04-25
revisions:
  - 2026-04-27
  - 2026-05-02
  - 2026-05-10
  - 2026-05-25
---

# Remove Duplicates From Sorted Array

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Google #Microsoft #Facebook #Adobe #Bloomberg

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

Two Pointers (Slow & Fast / Read & Write)

---
## Difficulty

Easy | #easy

---

## ⚡ Key Idea (Core Insight)

Since the array is **sorted**, all duplicate elements are adjacent. We can maintain a `slow` pointer that tracks the position of the last unique element found and a `fast` pointer that scans the array for the next unique value.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Use `slow` to mark the "unique boundary." Update `nums[++slow] = nums[fast]` only when `nums[fast] != nums[slow]`. Return `slow + 1`.

---

## Approach

### Brute Force
- Copy elements into a `Set` to handle uniqueness, then overwrite the original array.
- **Time:** O(N) | **Space:** O(N)

### Better (Not applicable)
- The two-pointer approach is the standard optimal for in-place requirements.

### Optimal
1. Handle edge case: if array length is 0, return 0.
2. Initialize `slow = 0`.
3. Iterate `fast` from `1` to `N-1`.
4. If `nums[fast] != nums[slow]`:
   - Increment `slow`.
   - Copy `nums[fast]` to `nums[slow]`.
5. Return `slow + 1` (the count of unique elements).

---

## Code (Python)

```python
class Solution:
    def removeDuplicates(self, nums: list[int]) -> int:
        if not nums:
            return 0
        
        # slow pointer tracks the index of the last unique element
        slow = 0
        
        # fast pointer explores the array
        for fast in range(1, len(nums)):
            # Found a new unique element
            if nums[fast] != nums[slow]:
                slow += 1
                nums[slow] = nums[fast]
        
        # Length is slow index + 1
        return slow + 1
```

---

## Dry Run (Smart Example)

**Input:** `nums = [1, 1, 2, 3, 3]`

| Step | Fast | Slow | Comparison (`nums[f] != nums[s]`) | Action | Array State |
| :--- | :--- | :--- | :--- | :--- | :--- |
| Init | - | 0 | - | - | `[1, 1, 2, 3, 3]` |
| 1 | 1 | 0 | `1 != 1` (False) | Skip | `[1, 1, 2, 3, 3]` |
| 2 | 2 | 1 | `2 != 1` (True) | `nums[1] = 2` | `[1, 2, 2, 3, 3]` |
| 3 | 3 | 2 | `3 != 2` (True) | `nums[2] = 3` | `[1, 2, 3, 3, 3]` |
| 4 | 4 | 2 | `3 != 3` (False) | Skip | `[1, 2, 3, 3, 3]` |

**Result:** `slow + 1 = 3`. Unique array prefix: `[1, 2, 3]`.

---

## Edge Cases

- **Empty Array:** Handled by `if not nums` (returns 0).
- **No Duplicates:** `slow` will increment every time; array remains same.
- **All Duplicates:** `slow` stays at 0; returns 1.
- **Single Element:** Loop doesn't run; returns 1.

---

## Mistakes

- **Returning `slow` instead of `slow + 1`:** Remember `slow` is an index, but we need the count/length.
- **Starting `fast` at 0:** This causes an unnecessary comparison of `nums[0]` with itself.
- **Using extra space:** Do not use a result list or set; the problem usually mandates O(1) space.
- **User mistake:** No specific note provided. (Ensure you define the pointers clearly before coding).

---

## Complexity

- **Time:** O(N) → We traverse the array exactly once with the `fast` pointer.
- **Space:** O(1) → We modify the array in-place without auxiliary data structures.

---

## Similar Problems

- [Remove Element](https://leetcode.com/problems/remove-element/) - Easy
- [Remove Duplicates from Sorted Array II](https://leetcode.com/problems/remove-duplicates-from-sorted-array-ii/) - Medium
- [Move Zeroes](https://leetcode.com/problems/move-zeroes/) - Easy
- [Apply Operations to an Array](https://leetcode.com/problems/apply-operations-to-an-array/) - Easy

---

## Tags and Properties
- #dsa #important #revisit #arrays #leetcode26
- [[Two Pointers]] [[Array Manipulation]]
- Revision Date: 2026-04-25
- **Problem Link:** [LeetCode #26 - Remove Duplicates From Sorted Array](https://leetcode.com/problems/remove-duplicates-from-sorted-array/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-27)
- [ ] Day 7 Revision (2026-05-02)
- [ ] Day 15 Revision (2026-05-10)
- [ ] Day 30 Revision (2026-05-25)
