---
created: 2026-04-06
revisions:
  - 2026-04-08
  - 2026-04-13
  - 2026-04-21
  - 2026-05-06
---

# Bubble Sort

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Microsoft #Adobe #Amazon #HCL #TCS

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #sorting [[Sorting]]
  - #arrays [[Arrays]]
  - #in-place [[In-Place Algorithms]]

## Pattern

Adjacent Comparisons + In-place Swapping  

---
## Difficulty

Easy  
#easy

---

## ⚡ Key Idea (Core Insight)

The algorithm repeatedly steps through the list, compares **adjacent elements**, and swaps them if they are in the wrong order. In each complete pass, the **largest unsorted element** "bubbles up" to its correct position at the end of the array.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Compare `arr[j]` and `arr[j+1]`. If `left > right`, swap. Largest element "sinks" to the back every iteration.

---

## Approach

### Brute Force
- Run two nested loops. Inner loop compares all adjacent pairs regardless of whether the array is already sorted.
- **Time Complexity:** $O(N^2)$

### Better (Early Exit Optimization)
- Introduce a `swapped` boolean flag. 
- If no two elements were swapped during the inner loop pass, the array is already sorted—break immediately.
- **Improvement:** Reduces best-case time complexity to $O(N)$.

### Optimal
- The "Better" approach is the standard optimal version for Bubble Sort.
- Ensure the inner loop range decreases by `i` each time (as the last `i` elements are already in place).

---

## Code (Python)

```python
def bubble_sort(arr):
    n = len(arr)
    for i in range(n):
        # Flag to check if any swapping happened
        swapped = False
        
        # Last i elements are already in place
        for j in range(0, n - i - 1):
            if arr[j] > arr[j + 1]:
                # Swap if the element found is greater than the next
                arr[j], arr[j + 1] = arr[j + 1], arr[j]
                swapped = True
        
        # If no two elements were swapped by inner loop, then break
        if not swapped:
            break
    return arr
```

---

## Dry Run (Smart Example)

**Input:** `[4, 2, 4, 1]` (Includes duplicates)

| Step | Current State | Variables | Explanation |
| :--- | :--- | :--- | :--- |
| 1 | `[2, 4, 4, 1]` | `i=0, j=0` | `4 > 2`, swap. |
| 2 | `[2, 4, 4, 1]` | `i=0, j=1` | `4 == 4`, no swap. |
| 3 | `[2, 4, 1, 4]` | `i=0, j=2` | `4 > 1`, swap. Largest `4` is at end. |
| 4 | `[2, 1, 4, 4]` | `i=1, j=0` | `2 > 1`, swap. Second largest `4` is at end. |
| 5 | `[1, 2, 4, 4]` | `i=2` | Pass starts, `swapped` remains `False`. |

---

## Edge Cases

- **Already Sorted:** `[1, 2, 3, 4]` — Handled by `swapped` flag in $O(N)$.
- **Reverse Sorted:** `[4, 3, 2, 1]` — Maximum swaps required, $O(N^2)$.
- **Single Element:** `[1]` — Loop condition `n-i-1` handles this safely.
- **All Duplicates:** `[2, 2, 2]` — No swaps occur, exits in $O(N)$.

---

## Mistakes

- **Inner Loop Range:** Running the inner loop to `n-1` instead of `n-i-1` (unnecessary comparisons).
- **Early Exit:** Forgetting the `swapped` flag, making the best case $O(N^2)$ instead of $O(N)$.
- **Stability:** Using `>=` instead of `>` in the comparison, which breaks algorithm stability.
- **User Mistake:** No specific note provided.

---

## Complexity

- **Time:** $O(N^2)$ → Average and Worst case due to nested loops; $O(N)$ Best case with flag.
- **Space:** $O(1)$ → Performed in-place without auxiliary data structures.

---

## Tags and Properties

- #dsa #important #revisit  
- #sorting [[Sorting]] #algorithms [[Algorithms]]
- **Revision Date:** 2026-04-06
- **Related:** [[Selection Sort]], [[Insertion Sort]]

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-08)
- [ ] Day 7 Revision (2026-04-13)
- [ ] Day 15 Revision (2026-04-21)
- [ ] Day 30 Revision (2026-05-06)
