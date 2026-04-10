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

Adjacent Comparison + In-place Swapping

---
## Difficulty

Easy  
#easy

---

## ⚡ Key Idea (Core Insight)

Iteratively compare adjacent elements and swap them if they are in the wrong order. In each pass, the largest unsorted element "bubbles up" to its correct position at the end of the array.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Compare `arr[j]` and `arr[j+1]`; swap if `arr[j] > arr[j+1]`. Use a `swapped` flag to exit early if no swaps occur (array is already sorted).

---

## Approach

### Brute Force
- Run two nested loops $N$ times regardless of array state.
- Time Complexity: $O(N^2)$
- Space Complexity: $O(1)$

### Better / Optimal
- **Optimization:** Introduce a boolean flag `swapped`. If the inner loop completes without any swaps, the array is already sorted—break early.
- Inner loop range reduces by 1 in each outer iteration (`n - i - 1`) as the end is already sorted.

---

## Code (Python)

```python
class Solution:
    def bubbleSort(self, arr: list[int]) -> list[int]:
        n = len(arr)
        # Outer loop for number of passes
        for i in range(n):
            swapped = False
            # Inner loop for adjacent comparisons
            # Last i elements are already in place
            for j in range(0, n - i - 1):
                if arr[j] > arr[j + 1]:
                    # Swap if elements are in wrong order
                    arr[j], arr[j + 1] = arr[j + 1], arr[j]
                    swapped = True
            
            # If no two elements were swapped by inner loop, then break
            if not swapped:
                break
        return arr
```

---

## Dry Run (Smart Example)

**Input:** `[5, 1, 4, 2, 8]`

| Step | Variables (i, j) | Array State | Explanation |
| :--- | :--- | :--- | :--- |
| 1.1 | i=0, j=0 | `[1, 5, 4, 2, 8]` | 5 > 1, Swap |
| 1.2 | i=0, j=1 | `[1, 4, 5, 2, 8]` | 5 > 4, Swap |
| 1.3 | i=0, j=2 | `[1, 4, 2, 5, 8]` | 5 > 2, Swap |
| 1.4 | i=0, j=3 | `[1, 4, 2, 5, 8]` | 5 < 8, No Swap. 8 is locked at end. |
| 2.1 | i=1, j=1 | `[1, 2, 4, 5, 8]` | 4 > 2, Swap. |
| 3.1 | i=2 | `[1, 2, 4, 5, 8]` | No swaps in pass i=2. Break early. |

---

## Edge Cases

- **Already Sorted:** `[1, 2, 3, 4, 5]` -> Optimized version finishes in $O(N)$.
- **Reverse Sorted:** `[5, 4, 3, 2, 1]` -> Requires maximum swaps $O(N^2)$.
- **All Identical:** `[2, 2, 2]` -> Finishes in one pass $O(N)$.
- **Single Element:** `[1]` -> Loop doesn't execute; returns correctly.
- **Negative Numbers:** `[-2, -5, 1, 0]` -> Handled correctly by standard comparison.

---

## Mistakes

- **Inner Loop Range:** Forgetting to use `n - i - 1`, leading to unnecessary comparisons or index errors.
- **Missing Optimization:** Failing to implement the `swapped` flag, making the Best Case $O(N^2)$ instead of $O(N)$.
- **User Mistake:** No specific note provided.

---

## Complexity

- **Time:** $O(N^2)$ Worst/Average; $O(N)$ Best case with optimization.  
- **Space:** $O(1)$ constant space as sorting is done in-place.

---

## Similar Problems

- [Selection Sort](https://www.geeksforgeeks.org/selection-sort/) - Easy
- [Insertion Sort](https://leetcode.com/problems/insertion-sort-list/) - Medium (List version)
- [Sort Colors](https://leetcode.com/problems/sort-colors/) - Medium

---

## Tags and Properties
  - #dsa #important #revisit #sorting #arrays
  - [[Sorting]] [[Array]]
  - **Revision Date:** 2026-04-10
  - **Problem Link:** [Bubble Sort - GeeksforGeeks](https://www.geeksforgeeks.org/problems/bubble-sort/1)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-12)
- [ ] Day 7 Revision (2026-04-17)
- [ ] Day 15 Revision (2026-04-25)
- [ ] Day 30 Revision (2026-05-10)
