---
created: 2026-04-25
revisions:
  - 2026-04-27
  - 2026-05-02
  - 2026-05-10
  - 2026-05-25
---

# Quick Sort

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Google #Microsoft #Meta #Adobe #GoldmanSachs

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #sorting [[Sorting]]
  - #divideandconquer [[Divide and Conquer]]
  - #recursion [[Recursion]]

---
## Pattern

Divide and Conquer + Partitioning (Lomuto or Hoare)

---
## Difficulty

Medium  
#medium

---

## ⚡ Key Idea (Core Insight)

Pick a **pivot** element and rearrange the array so that all elements smaller than the pivot are to its left and all larger elements are to its right. Recursively apply this logic to the sub-arrays.

---

## ⚡ Quick Recall (VERY IMPORTANT)

**Partitioning is the engine:** Pivot finds its final sorted position in every "Divide" step.

---

## Approach

### Brute Force
- Create two new lists (`left`, `right`), iterate through the array, append elements based on pivot comparison, and concatenate.
- Time: O(N log N) average | Space: O(N) additional memory.

### Optimal (In-place)
- Use a **partitioning algorithm** (Lomuto is standard) to swap elements within the original array.
- Use a `pointer` to track the boundary of elements smaller than the pivot.
- Recursively sort indices `[low, pivot_idx - 1]` and `[pivot_idx + 1, high]`.

---

## Code (Python)

```python
class Solution:
    def sortArray(self, nums: list[int]) -> list[int]:
        """
        Standard Quick Sort implementation using Lomuto Partition.
        """
        self.quickSort(nums, 0, len(nums) - 1)
        return nums

    def quickSort(self, nums: list[int], low: int, high: int):
        if low < high:
            # p_idx is the partitioning index, nums[p_idx] is at right place
            p_idx = self.partition(nums, low, high)
            
            # Separately sort elements before and after partition
            self.quickSort(nums, low, p_idx - 1)
            self.quickSort(nums, p_idx + 1, high)

    def partition(self, nums: list[int], low: int, high: int) -> int:
        # Picking the last element as pivot
        pivot = nums[high]
        i = low - 1  # Index of smaller element
        
        for j in range(low, high):
            # If current element is smaller than or equal to pivot
            if nums[j] <= pivot:
                i += 1
                nums[i], nums[j] = nums[j], nums[i]
        
        # Place pivot in the correct sorted position
        nums[i + 1], nums[high] = nums[high], nums[i + 1]
        return i + 1
```

---

## Dry Run (Smart Example)

Input: `nums = [3, -1, 3, 2]`, low=0, high=3, pivot = 2 (last element)

| Step | i (boundary) | j (iterator) | State of `nums` | Explanation |
| :--- | :--- | :--- | :--- | :--- |
| Init | -1 | 0 | `[3, -1, 3, 2]` | Pivot is 2. |
| 1 | -1 | 0 | `[3, -1, 3, 2]` | `3 > 2`, no swap. |
| 2 | 0 | 1 | `[-1, 3, 3, 2]` | `-1 <= 2`, i becomes 0, swap `nums[0]` & `nums[1]`. |
| 3 | 0 | 2 | `[-1, 3, 3, 2]` | `3 > 2`, no swap. |
| Final | 0 | - | `[-1, 2, 3, 3]` | Loop ends. Swap `nums[i+1]` with pivot. |

---

## Edge Cases

- **Already Sorted:** Leads to $O(N^2)$ if pivot is always the last/first element.
- **All Elements Identical:** Partitioning might become unbalanced.
- **Reverse Sorted:** Similar to sorted, causes worst-case recursion depth.
- **Empty or Single Element:** Handled by `low < high` base case.

---

## Mistakes

- **Unstable Pivot:** Not using a randomized pivot in production, leading to $O(N^2)$ on sorted data.
- **Off-by-one:** Incorrectly setting ranges in recursive calls (e.g., including `p_idx` in both).
- **Stack Overflow:** Not considering recursion depth for extremely large, skewed arrays.
- **User Mistake:** No specific note provided (Initial documentation gap).

---

## Complexity

Time: O(N log N) Average, O(N²) Worst → Average case assumes balanced splits; worst case occurs on sorted/near-sorted arrays with naive pivot.  
Space: O(log N) Average, O(N) Worst → This is the recursion stack depth.

---

## Similar Problems

- [Sort an Array](https://leetcode.com/problems/sort-an-array/) - Medium
- [Kth Largest Element in an Array](https://leetcode.com/problems/kth-largest-element-in-an-array/) - Medium (Quick Select)
- [K Closest Points to Origin](https://leetcode.com/problems/k-closest-points-to-origin/) - Medium

---

## Tags and Properties
- #dsa #important #revisit #sorting #divideandconquer
- [[Sorting]] [[Divide and Conquer]] [[Recursion]]
- **Revision Date:** 2026-04-25
- **Problem Link:** [LeetCode Sort an Array](https://leetcode.com/problems/sort-an-array/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-27)
- [ ] Day 7 Revision (2026-05-02)
- [ ] Day 15 Revision (2026-05-10)
- [ ] Day 30 Revision (2026-05-25)
