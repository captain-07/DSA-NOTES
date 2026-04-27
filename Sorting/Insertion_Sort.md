---
created: 2026-04-25
revisions:
  - 2026-04-27
  - 2026-05-02
  - 2026-05-10
  - 2026-05-25
---

# Insertion Sort

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Microsoft #Google #TCS #Infosys (Common in foundational/online assessments)

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #sorting [[Sorting]]
  - #arrays [[Arrays]]
  - #incremental [[Incremental Construction]]

---
## Pattern

Incremental Construction (Building a sorted subarray one element at a time)

---
## Difficulty

Easy / #easy

---

## ⚡ Key Idea (Core Insight)

Divides the array into **Sorted** and **Unsorted** partitions. It picks the first element from the unsorted part and "shuffles" it back into its correct relative position within the sorted part by shifting larger elements to the right.

---

## ⚡ Quick Recall (VERY IMPORTANT)

**"Card Shuffling"**: Picking a card and sliding it into its correct spot among the cards already in your hand.

---

## Approach

### Brute Force
- Standard implementation is already considered the "naive" sorting approach.
- Time: $O(n^2)$

### Better (Binary Insertion Sort)
- Use **Binary Search** to find the correct insertion index instead of linear scanning.
- **Improvement:** Reduces comparisons to $O(n \log n)$, but total shifts remain $O(n^2)$.

### Optimal (Standard In-Place)
1. Iterate from $i = 1$ to $n-1$.
2. Store current element as `key`.
3. Compare `key` with elements in the sorted partition (to the left).
4. Shift elements greater than `key` one position to the right.
5. Insert `key` into its hole.

---

## Code (Python)

```python
class Solution:
    def insertionSort(self, nums: list[int]) -> list[int]:
        # Iterate from the second element to the end
        for i in range(1, len(nums)):
            key = nums[i]
            j = i - 1
            
            # Shift elements of nums[0..i-1] that are greater than key
            # to one position ahead of their current position
            while j >= 0 and nums[j] > key:
                nums[j + 1] = nums[j]
                j -= 1
            
            # Place the key at its correct position
            nums[j + 1] = key
            
        return nums
```

---

## Dry Run (Smart Example)

**Input:** `[5, 2, 9, 1, 5]`

| Step | i | Key | Variables/Action | Array State |
| :--- | :- | :-- | :--- | :--- |
| 1 | 1 | 2 | $5 > 2$, shift 5 right | `[2, 5, 9, 1, 5]` |
| 2 | 2 | 9 | $5 < 9$, no shift | `[2, 5, 9, 1, 5]` |
| 3 | 3 | 1 | Shift 9, 5, 2 right | `[1, 2, 5, 9, 5]` |
| 4 | 4 | 5 | $9 > 5$, shift 9 right; $5 == 5$, stop | `[1, 2, 5, 5, 9]` |

---

## Edge Cases

- **Already Sorted:** $O(n)$ time (Best Case) - only one comparison per element.
- **Reverse Sorted:** $O(n^2)$ time (Worst Case) - maximum shifts.
- **Duplicates:** Stable sorting algorithm - preserves relative order of duplicate elements.
- **Single Element/Empty:** Handled naturally by `range(1, n)`.

---

## Mistakes

- **Incorrect Loop Bounds:** Starting the outer loop at 0 instead of 1.
- **Overwriting the Key:** Forgetting to store `nums[i]` in a variable before shifting.
- **Off-by-one in While:** Using `j > 0` instead of `j >= 0`.
- **Inefficiency:** Not breaking the inner loop when `nums[j] <= key`.
- **User Mistake:** No specific note provided for previous attempts.

---

## Complexity

- **Time:** $O(n^2)$ Average/Worst; $O(n)$ Best Case (if array is nearly sorted).
- **Space:** $O(1)$ In-place sorting.

---

## Similar Problems

- [Sort Colors](https://leetcode.com/problems/sort-colors/) - Medium
- [Sort List](https://leetcode.com/problems/sort-list/) - Medium (Often solved with Merge Sort, but Insertion Sort is viable for small lists)
- [Insertion Sort List](https://leetcode.com/problems/insertion-sort-list/) - Medium
- [Selection Sort](https://www.geeksforgeeks.org/selection-sort/) - Easy

---

## Tags and Properties

- #dsa #important #revisit #sorting
- [[Sorting]] [[Arrays]] [[In-Place Algorithms]]
- **Revision Date:** 2026-04-25
- **Problem Link:** [LeetCode: Insertion Sort List](https://leetcode.com/problems/insertion-sort-list/) (Logic applies here) | [GeeksforGeeks: Insertion Sort](https://www.geeksforgeeks.org/insertion-sort/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-27)
- [ ] Day 7 Revision (2026-05-02)
- [ ] Day 15 Revision (2026-05-10)
- [ ] Day 30 Revision (2026-05-25)
