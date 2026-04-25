---
created: 2026-04-25
revisions:
  - 2026-04-27
  - 2026-05-02
  - 2026-05-10
  - 2026-05-25
---

# Next Permutation

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Google #Microsoft #Meta #Adobe #Uber

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #arrays [[Arrays]]
  - #permutations [[Permutations]]
  - #lexicographical [[Lexicographical Order]]

---
## Pattern

Lexicographical Suffix Manipulation (Pivot + Successor)

---
## Difficulty

Medium  
#medium

---

## ⚡ Key Idea (Core Insight)

To find the smallest increment in lexicographical order:
1. Identify the **rightmost dip** (pivot point) where the ascending order from the right breaks.
2. Swap this pivot with the **smallest element larger than it** to its right.
3. Reverse the suffix to the right of the pivot to make it as small as possible (ascending).

---

## ⚡ Quick Recall (VERY IMPORTANT)

Find the **first `i` from right** such that `arr[i] < arr[i+1]`. Swap `arr[i]` with the **next larger element** to its right, then **reverse** everything after `i`.

---

## Approach

### Brute Force
- Generate all possible permutations, sort them, and find the one immediately after the input.
- **Time Complexity:** O(N! * N)
- **Space Complexity:** O(N!)

### Optimal
1. **Find Pivot:** Traverse from right to left to find the first index `i` such that `nums[i] < nums[i+1]`.
2. **Find Successor:** If pivot exists, traverse from right to left to find index `j` such that `nums[j] > nums[i]`.
3. **Swap:** Swap `nums[i]` and `nums[j]`.
4. **Reverse:** Reverse the subarray from `i + 1` to the end of the array.
- **Time Complexity:** O(N)
- **Space Complexity:** O(1)

---

## Code (Python)

```python
class Solution:
    def nextPermutation(self, nums: list[int]) -> None:
        """
        Do not return anything, modify nums in-place instead.
        """
        n = len(nums)
        pivot = -1
        
        # Step 1: Find the rightmost dip
        for i in range(n - 2, -1, -1):
            if nums[i] < nums[i + 1]:
                pivot = i
                break
        
        # If no pivot, the array is in descending order; reverse all
        if pivot == -1:
            nums.reverse()
            return
        
        # Step 2: Find the successor to the pivot
        for j in range(n - 1, pivot, -1):
            if nums[j] > nums[pivot]:
                nums[pivot], nums[j] = nums[j], nums[pivot]
                break
        
        # Step 3: Reverse the suffix to get the smallest possible tail
        left, right = pivot + 1, n - 1
        while left < right:
            nums[left], nums[right] = nums[right], nums[left]
            left += 1
            right -= 1
```

---

## Dry Run (Smart Example)

**Input:** `[1, 5, 8, 4, 7, 6, 5, 3, 1]`

| Step | Variables | Explanation |
| :--- | :--- | :--- |
| 1. Find Pivot | `i = 3` (val=4) | `nums[3]=4 < nums[4]=7`. 4 is the pivot. |
| 2. Find Successor| `j = 6` (val=5) | From right, 5 is the first element > 4. |
| 3. Swap | `nums[3], nums[6]` | Array becomes `[1, 5, 8, 5, 7, 6, 4, 3, 1]` |
| 4. Reverse Suffix| `Reverse index 4 to 8` | Suffix `[7, 6, 4, 3, 1]` becomes `[1, 3, 4, 6, 7]` |
| **Result** | `[1, 5, 8, 5, 1, 3, 4, 6, 7]` | Lexicographically next permutation. |

---

## Edge Cases

- **Strictly Decreasing:** `[3, 2, 1]` → Reverses to `[1, 2, 3]`.
- **Strictly Increasing:** `[1, 2, 3]` → Swaps last two to `[1, 3, 2]`.
- **Duplicates:** `[1, 1, 5]` → Correctly finds pivot and next larger element.
- **Single Element:** `[1]` → No change.

---

## Mistakes

- Forgetting to handle the "all descending" case (should reverse the whole array).
- Swapping the pivot with the first element from the right instead of the *smallest larger* element.
- Failing to reverse the suffix after the swap (leaving it in descending order makes it the *largest* possible, not *smallest*).
- **User Mistake:** No specific note provided (ensure comprehensive logic coverage).

---

## Complexity

- **Time:** O(N) → Three linear passes: find pivot, find successor, reverse suffix.
- **Space:** O(1) → In-place modification of the input array.

---

## Similar Problems

- [Permutations](https://leetcode.com/problems/permutations/) - Medium
- [Permutation Sequence](https://leetcode.com/problems/permutation-sequence/) - Hard
- [Next Greater Element III](https://leetcode.com/problems/next-greater-element-iii/) - Medium
- [Previous Permutation With One Swap](https://leetcode.com/problems/previous-permutation-with-one-swap/) - Medium

---

## Tags and Properties
- #dsa #important #revisit #arrays #math 
- [[Arrays]], [[Two Pointers]]
- **Revision Date:** April 25, 2026
- **Problem Link:** [LeetCode - Next Permutation](https://leetcode.com/problems/next-permutation/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-27)
- [ ] Day 7 Revision (2026-05-02)
- [ ] Day 15 Revision (2026-05-10)
- [ ] Day 30 Revision (2026-05-25)
