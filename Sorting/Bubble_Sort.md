---
created: 2026-04-11
revisions:
  - 2026-04-13
  - 2026-04-18
  - 2026-04-26
  - 2026-05-11
---

# Bubble Sort

---

## Pattern

Iterative Comparison + Adjacent Swapping

---
## Difficulty

Easy #easy

---

## ⚡ Key Idea (Core Insight)

The algorithm repeatedly steps through the list, compares adjacent elements, and swaps them if they are in the wrong order. In each complete pass, the largest unsorted element "bubbles up" to its correct final position at the end of the array.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Compare neighbors and swap if `arr[j] > arr[j+1]`; use a `swapped` flag for $O(n)$ early exit.

---

## Approach

### Brute Force
- Nested loops: Outer loop runs $N$ times, inner loop compares all adjacent pairs.
- Time: $O(n^2)$
- Space: $O(1)$

### Better (Optimized)
- Introduce a `swapped` boolean. If no elements are swapped during an entire inner loop pass, the array is already sorted.
- Time: $O(n)$ best case.

### Optimal
- For Bubble Sort, the optimized version is the standard "optimal" implementation.
- Step 1: Iterate $i$ from $0$ to $n-1$.
- Step 2: Iterate $j$ from $0$ to $n-i-2$ (avoiding already sorted tail).
- Step 3: Swap if `arr[j] > arr[j+1]`.
- Step 4: If no swaps occurred, terminate early.

---

## Code (Python)

```python
class Solution:
    def bubbleSort(self, arr: list[int]) -> list[int]:
        n = len(arr)
        for i in range(n):
            # Flag to optimize: check if any swap happened in this pass
            swapped = False
            
            # Last i elements are already in their correct place
            for j in range(0, n - i - 1):
                # Compare adjacent elements
                if arr[j] > arr[j+1]:
                    # Swap if they are in the wrong order
                    arr[j], arr[j+1] = arr[j+1], arr[j]
                    swapped = True
            
            # If no two elements were swapped, array is sorted
            if not swapped:
                break
        return arr
```

---

## Dry Run (Smart Example)

**Input:** `[4, -2, 4, 1]` (Duplicates + Negatives)

| Step | Variables | Explanation |
| :--- | :--- | :--- |
| Pass 1 | `i=0, j=0` | `4 > -2`: Swap. Arr: `[-2, 4, 4, 1]` |
| Pass 1 | `i=0, j=1` | `4 > 4`: No Swap (Stability preserved). Arr: `[-2, 4, 4, 1]` |
| Pass 1 | `i=0, j=2` | `4 > 1`: Swap. Arr: `[-2, 4, 1, 4]` |
| Pass 2 | `i=1, j=0` | `-2 < 4`: No Swap. Arr: `[-2, 4, 1, 4]` |
| Pass 2 | `i=1, j=1` | `4 > 1`: Swap. Arr: `[-2, 1, 4, 4]` |
| Pass 3 | `i=2, j=0` | `-2 < 1`: No Swap. `swapped` stays `False`. |
| End | Early Break | `swapped` was `False` in Pass 3. Return `[-2, 1, 4, 4]`. |

---

## Edge Cases

- **Already Sorted:** `[1, 2, 3, 4]` -> $O(n)$ time due to early exit flag.
- **Reverse Sorted:** `[4, 3, 2, 1]` -> Maximum swaps ($n(n-1)/2$).
- **All Elements Same:** `[5, 5, 5, 5]` -> $O(n)$ time with flag.
- **Single Element:** `[1]` -> Loops handle range correctly, no action taken.

---

## Mistakes

- **Incorrect Inner Bound:** Using `n-1` instead of `n-i-1`, leading to redundant comparisons or IndexOutOfBounds.
- **Missing Optimization:** Forgetting the `swapped` flag, making the best case $O(n^2)$ instead of $O(n)$.
- **Stability Break:** Using `>=` instead of `>` in the comparison, which breaks the stable sorting property.
- **User mistake:** No specific note provided.

---

## Complexity

Time: $O(n^2)$ → Average/Worst case due to nested loops. $O(n)$ Best case (already sorted).  
Space: $O(1)$ → In-place sorting; no auxiliary data structures used.

---

## Similar Problems

- [Sort Colors](https://leetcode.com/problems/sort-colors/) - Medium
- [Insertion Sort List](https://leetcode.com/problems/insertion-sort-list/) - Medium
- [Selection Sort](https://practice.geeksforgeeks.org/problems/selection-sort/1) - Easy

---

## Tags and Properties
  - #dsa #important #revisit  
  - #sorting #arrays #bubble-sort
  - [[Sorting]] [[Arrays]]
  - Revision Date: 2026-04-11
  - **Problem Link:** [Bubble Sort - GeeksforGeeks](https://www.geeksforgeeks.org/problems/bubble-sort/1)

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Microsoft #Infosys #TCS #Wipro

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #sorting [[Sorting]], #arrays [[Arrays]], #stable-sort [[Stable Sort]]

---

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-13)
- [ ] Day 7 Revision (2026-04-18)
- [ ] Day 15 Revision (2026-04-26)
- [ ] Day 30 Revision (2026-05-11)
