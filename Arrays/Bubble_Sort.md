---
created: 2026-04-07
revisions:
  - 2026-04-09
  - 2026-04-14
  - 2026-04-22
  - 2026-05-07
---

# Bubble Sort

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Microsoft #Adobe #TCS #Infosys #Wipro

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #sorting [[Sorting]], #arrays [[Arrays]]

## Pattern

In-place Sorting + Adjacent Swapping  

---
## Difficulty

Easy #easy

---

## ⚡ Key Idea (Core Insight)

Repeatedly step through the list, compare adjacent elements, and swap them if they are in the wrong order. In each pass, the largest unsorted element "bubbles up" to its correct position at the end of the array.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Adjacent swaps; largest element moves to the end per pass. Optimized version stops early if no swaps occur.

---

## Approach

### Brute Force
- Run two nested loops $n$ times regardless of array state.
- Time Complexity: $O(n^2)$

### Optimal (Optimized Bubble Sort)
- **Logic:** Use a `swapped` boolean flag. If a pass completes without any swaps, the array is already sorted, so we break early.
- **Pass reduction:** After $i$ passes, the last $i$ elements are already in place, so the inner loop only needs to run up to $n-i-1$.

---

## Code (Python)

```python
def bubble_sort(arr):
    n = len(arr)
    # Outer loop for number of passes
    for i in range(n):
        swapped = False
        # Inner loop for adjacent comparisons
        # n-i-1 because last i elements are already sorted
        for j in range(0, n - i - 1):
            if arr[j] > arr[j + 1]:
                # Swap elements
                arr[j], arr[j + 1] = arr[j + 1], arr[j]
                swapped = True
        
        # If no elements were swapped by inner loop, then break
        if not swapped:
            break
    return arr
```

---

## Dry Run (Smart Example)

**Input:** `[5, 1, 4, 2, 8]`

| Step | i, j | Array State | Explanation |
| :--- | :--- | :--- | :--- |
| 1 | i=0, j=0 | `[1, 5, 4, 2, 8]` | 5 > 1, swap. |
| 2 | i=0, j=1 | `[1, 4, 5, 2, 8]` | 5 > 4, swap. |
| 3 | i=0, j=2 | `[1, 4, 2, 5, 8]` | 5 > 2, swap. |
| 4 | i=0, j=3 | `[1, 4, 2, 5, 8]` | 5 < 8, no swap. 8 is now "bubbled" to end. |
| 5 | i=1, j=0 | `[1, 4, 2, 5, 8]` | 1 < 4, no swap. |
| 6 | i=1, j=1 | `[1, 2, 4, 5, 8]` | 4 > 2, swap. 5 and 8 are sorted. |

---

## Edge Cases

- **Already Sorted:** $O(n)$ time with optimized flag.
- **Reverse Sorted:** Maximum swaps required, $O(n^2)$.
- **Single Element:** Loop terminates immediately.
- **Duplicate Elements:** Stable sort (maintains relative order of equal elements).

---

## Mistakes

- **Inner Loop Bounds:** Forgetting to use `n - i - 1`, leading to redundant comparisons or IndexOutOfBounds.
- **Optimization:** Missing the `swapped` flag, causing $O(n^2)$ even on sorted input.
- **User Mistake:** No specific note provided.

---

## Complexity

Time: O($n^2$) → Average and Worst case due to nested loops. $O(n)$ Best case with optimized flag.  
Space: O(1) → In-place sorting; no extra memory used beyond variables.

---

## Similar Problems

- [Selection Sort](https://www.geeksforgeeks.org/selection-sort/) - Easy
- [Insertion Sort](https://www.geeksforgeeks.org/insertion-sort/) - Easy
- [Sort Colors (Dutch National Flag)](https://leetcode.com/problems/sort-colors/) - Medium
- [Sort an Array](https://leetcode.com/problems/sort-an-array/) - Medium

---

## Tags and Properties

- #dsa #important #revisit #sorting #arrays
- [[Sorting]] [[Arrays]]
- **Revision Date:** 2026-04-07
- **Problem Link:** [GeeksforGeeks - Bubble Sort](https://www.geeksforgeeks.org/bubble-sort-algorithms-by-using-python-language/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-09)
- [ ] Day 7 Revision (2026-04-14)
- [ ] Day 15 Revision (2026-04-22)
- [ ] Day 30 Revision (2026-05-07)
