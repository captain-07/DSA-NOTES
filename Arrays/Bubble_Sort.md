---
created: 2026-04-10
revisions:
  - 2026-04-12
  - 2026-04-17
  - 2026-04-25
  - 2026-05-10
---

# Bubble Sort

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Microsoft #Samsung #Adobe #Infosys #TCS

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #sorting [[Sorting]], #arrays [[Arrays]]

## Pattern

- Adjacent Comparison + Swapping (Sinking Sort)

---
## Difficulty

Easy  
#easy

---

## ⚡ Key Idea (Core Insight)

Iteratively compare adjacent elements and swap them if they are in the wrong order. In each pass, the largest unsorted element "bubbles up" to its correct final position at the end of the array.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Compare `arr[j]` and `arr[j+1]`; swap if `arr[j] > arr[j+1]`. Use a `swapped` flag to exit early if the array becomes sorted.

---

## Approach

### Brute Force
- Run two nested loops: outer loop `n` times, inner loop `n-1` times.
- Time: O(n²) | Space: O(1)

### Optimal (Adaptive)
- **Optimization 1:** The inner loop only needs to run up to `n - i - 1` because the last `i` elements are already sorted.
- **Optimization 2:** Use a `swapped` boolean. If no swaps occur in a pass, the array is sorted; break immediately.
- Time: O(n²) worst/average, O(n) best case | Space: O(1)

---

## Code (Python)

```python
class Solution:
    def bubbleSort(self, arr: list[int]) -> list[int]:
        n = len(arr)
        
        for i in range(n):
            # Flag to check if any swapping happened in this pass
            swapped = False
            
            # Last i elements are already in place
            for j in range(0, n - i - 1):
                if arr[j] > arr[j + 1]:
                    # Swap adjacent elements
                    arr[j], arr[j + 1] = arr[j + 1], arr[j]
                    swapped = True
            
            # If no two elements were swapped by inner loop, then break
            if not swapped:
                break
                
        return arr
```

---

## Dry Run (Smart Example)

Input: `[5, -2, 9, 1, 5]` (Includes negative and duplicate)

| Step | Variables (i, j) | Array State | Explanation |
| :--- | :--- | :--- | :--- |
| 1 | i=0, j=0..3 | `[-2, 5, 1, 5, 9]` | 9 bubbles to the end. `swapped=True`. |
| 2 | i=1, j=0..2 | `[-2, 1, 5, 5, 9]` | 5 bubbles to second last. `swapped=True`. |
| 3 | i=2, j=0..1 | `[-2, 1, 5, 5, 9]` | No swaps needed for `[-2, 1, 5]`. `swapped=False`. |
| 4 | Exit | `[-2, 1, 5, 5, 9]` | `swapped` is False; break early. |

---

## Edge Cases

- **Already Sorted:** `[1, 2, 3, 4, 5]` → Handled by `swapped` flag (O(n)).
- **Reverse Sorted:** `[5, 4, 3, 2, 1]` → Takes full O(n²) iterations.
- **All Identical:** `[2, 2, 2]` → Handled by `swapped` flag after 1st pass.
- **Single Element:** `[1]` → Inner loop doesn't run; returns correctly.
- **Negative Numbers:** `[-5, -1, -10]` → Comparison logic remains identical.

---

## Mistakes

- **User Mistake:** No specific note provided.
- Forgetting the `swapped` optimization (makes best case O(n²) instead of O(n)).
- Incorrect inner loop boundary (running `j` to `n-1` instead of `n-i-1`).
- Using extra space unnecessarily (Bubble sort is strictly in-place).

---

## Complexity

Time: O(n²) → Two nested loops in the worst case (reverse sorted).  
Space: O(1) → In-place sorting, only a few variables used.

---

## Similar Problems

- [Sort Colors (Dutch National Flag)](https://leetcode.com/problems/sort-colors/) - Medium
- [Insertion Sort List](https://leetcode.com/problems/insertion-sort-list/) - Medium
- [Selection Sort](https://www.geeksforgeeks.org/selection-sort/) - Easy

---

## Tags and Properties
  - #dsa #important #revisit #sorting #inplace
  - [[Sorting]] [[Array]]
  - **Revision Date:** 2026-04-10
  - **Problem Link:** [LeetCode - Sort an Array](https://leetcode.com/problems/sort-an-array/) (Note: Use Bubble Sort logic for learning, though O(n log n) is required for submission)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-12)
- [ ] Day 7 Revision (2026-04-17)
- [ ] Day 15 Revision (2026-04-25)
- [ ] Day 30 Revision (2026-05-10)
