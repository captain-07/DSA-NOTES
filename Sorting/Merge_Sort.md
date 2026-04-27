---
created: 2026-04-25
revisions:
  - 2026-04-27
  - 2026-05-02
  - 2026-05-10
  - 2026-05-25
---

# Merge Sort

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Google #Amazon #Microsoft #Meta #Apple #Uber

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #sorting [[Sorting]]
  - #divideandconquer [[Divide and Conquer]]
  - #recursion [[Recursion]]

## Pattern

Divide and Conquer  

---
## Difficulty

Medium  
#medium

---

## ⚡ Key Idea (Core Insight)

- Divide the unsorted list into $n$ sub-lists, each containing one element (a list of one element is considered sorted).
- Repeatedly merge sub-lists to produce new sorted sub-lists until there is only one sub-list remaining.

---

## ⚡ Quick Recall (VERY IMPORTANT)

- "Divide to the smallest unit, then merge two sorted halves using two pointers."

---

## Approach

### Brute Force
- Comparisons like Bubble Sort or Selection Sort.
- Time: $O(N^2)$
- Space: $O(1)$

### Optimal
- **Divide:** Find the midpoint and split the array into two halves.
- **Conquer:** Recursively call Merge Sort on both halves.
- **Combine:** Merge the two sorted halves into a single sorted array using a temporary buffer.
- Time: $O(N \log N)$
- Space: $O(N)$

---

## Code (Python)

```python
class Solution:
    def sortArray(self, nums: list[int]) -> list[int]:
        if len(nums) <= 1:
            return nums
        
        # 1. Divide
        mid = len(nums) // 2
        left_half = self.sortArray(nums[:mid])
        right_half = self.sortArray(nums[mid:])
        
        # 2. Conquer/Combine
        return self.merge(left_half, right_half)

    def merge(self, left: list[int], right: list[int]) -> list[int]:
        sorted_arr = []
        i = j = 0
        
        # Two-pointer merge logic
        while i < len(left) and j < len(right):
            if left[i] < right[j]:
                sorted_arr.append(left[i])
                i += 1
            else:
                sorted_arr.append(right[j])
                j += 1
        
        # Append remaining elements
        sorted_arr.extend(left[i:])
        sorted_arr.extend(right[j:])
        
        return sorted_arr
```

---

## Dry Run (Smart Example)

Input: `[3, 1, 4, 1]`

| Step | Action | State / Variables | Explanation |
| :--- | :--- | :--- | :--- |
| 1 | Split | `[3, 1]`, `[4, 1]` | Recursively divide into halves. |
| 2 | Split | `[3]`, `[1]`, `[4]`, `[1]` | Base case reached (size 1). |
| 3 | Merge | `left=[3], right=[1]` | Compare 3 & 1 $\rightarrow$ `[1, 3]`. |
| 4 | Merge | `left=[4], right=[1]` | Compare 4 & 1 $\rightarrow$ `[1, 4]`. |
| 5 | Merge | `left=[1, 3], right=[1, 4]` | Pointers: `1==1` (take right), `1<3` (take left), `3<4` (take left), `4` (rem) $\rightarrow$ `[1, 1, 3, 4]`. |

---

## Edge Cases

- **Empty Array:** `[]` returns `[]`.
- **Single Element:** `[1]` returns `[1]`.
- **Already Sorted:** `[1, 2, 3]` still takes $O(N \log N)$ time.
- **Duplicates:** `[2, 2, 2]` handled correctly by `<` or `<=` comparison.
- **Reverse Sorted:** `[5, 4, 3, 2, 1]` effectively handled by the merge logic.

---

## Mistakes

- **Space Complexity:** Forgetting that Merge Sort usually requires $O(N)$ extra space, unlike Quick Sort.
- **Stability:** Using `left[i] <= right[j]` vs `left[i] < right[j]` affects stability.
- **Slicing Cost:** In Python, `nums[:mid]` creates a copy, adding overhead. Use indices for true $O(N)$ space efficiency.
- **User Mistake:** No specific note provided.

---

## Complexity

Time: $O(N \log N)$ → Array is split $\log N$ times, and each level of merging takes $O(N)$ work.  
Space: $O(N)$ → Auxiliary space required for temporary arrays during the merge step.

---

## Similar Problems

- [Sort List](https://leetcode.com/problems/sort-list/) - Medium
- [Reverse Pairs](https://leetcode.com/problems/reverse-pairs/) - Hard
- [Count of Smaller Numbers After Self](https://leetcode.com/problems/count-of-smaller-numbers-after-self/) - Hard
- [Merge Sorted Array](https://leetcode.com/problems/merge-sorted-array/) - Easy

---

## Tags and Properties
- #dsa #important #revisit #mergesort #sorting
- [[Sorting]] [[Divide and Conquer]]
- **Problem Link:** [LeetCode - Sort an Array](https://leetcode.com/problems/sort-an-array/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-27)
- [ ] Day 7 Revision (2026-05-02)
- [ ] Day 15 Revision (2026-05-10)
- [ ] Day 30 Revision (2026-05-25)
