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
  - #Microsoft #Amazon #Samsung #Adobe #Infosys #TCS

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #sorting [[Sorting]], #arrays [[Arrays]]

## Pattern

In-place Comparison Sorting + Adjacent Swapping

---
## Difficulty

Easy  
#easy

---

## ⚡ Key Idea (Core Insight)

Repeatedly step through the list, compare adjacent elements, and swap them if they are in the wrong order. In each complete pass, the largest unsorted element "bubbles up" to its correct final position at the end of the array.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Compare `arr[j]` and `arr[j+1]`; swap if `arr[j] > arr[j+1]`. Use a `swapped` flag to break early if a pass completes without any swaps (array is already sorted).

---

## Approach

### Brute Force
- Run two nested loops: outer loop $N$ times, inner loop $N-1$ times. Always performs $O(N^2)$ comparisons.
- **Time Complexity:** $O(N^2)$

### Optimal (Early Exit)
- Outer loop runs from $i = 0$ to $N-1$.
- Inner loop runs from $j = 0$ to $N-i-2$ (ignoring already sorted elements at the end).
- Use a boolean flag `swapped`. If no elements are swapped in the inner loop, terminate immediately.
- **Time Complexity:** $O(N^2)$ worst, $O(N)$ best case.

---

## Code (Python)

```python
class Solution:
    def bubbleSort(self, arr: list[int]) -> list[int]:
        n = len(arr)
        # Outer loop for each pass
        for i in range(n):
            swapped = False
            # Inner loop for adjacent comparisons
            # n-i-1 because the last i elements are already sorted
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

| Step | Current Array | Explanation |
| :--- | :--- | :--- |
| **Start** | `[5, 1, 4, 2, 8]` | Initial unsorted array. |
| **Pass 1** | `[1, 4, 2, 5, 8]` | 5 swaps with 1, 4, 2. Largest element '8' was already at end. '5' is fixed. |
| **Pass 2** | `[1, 2, 4, 5, 8]` | 4 compares with 2 and swaps. '4' is fixed. |
| **Pass 3** | `[1, 2, 4, 5, 8]` | No swaps occur. `swapped` flag remains `False`. |
| **End** | `[1, 2, 4, 5, 8]` | Early exit triggered. Array sorted. |

---

## Edge Cases

- **Already Sorted Array:** `[1, 2, 3, 4, 5]` -> $O(N)$ time with early exit.
- **Reverse Sorted Array:** `[5, 4, 3, 2, 1]` -> Max number of swaps ($O(N^2)$).
- **Single Element/Empty Array:** Handled by loop ranges (no iterations).
- **Duplicates:** `[3, 1, 2, 1]` -> Correctly handles and maintains stability.
- **Negative Numbers:** `[-2, 5, -10, 0]` -> Comparison logic handles negatives correctly.

---

## Mistakes

- **User Mistake:** No specific note provided.
- Forgetting the `swapped` flag optimization (leads to unnecessary $O(N^2)$ on sorted data).
- Incorrect inner loop boundary (`n-i` vs `n-i-1`), causing `IndexOutOfBounds`.
- Thinking Bubble Sort is efficient for large datasets (it is almost never used in production).

---

## Complexity

**Time:** $O(N^2)$ → Average and worst case require nested iterations; $O(N)$ best case with optimization.  
**Space:** $O(1)$ → Performs swaps in-place without extra data structures.

---

## Similar Problems

- [Sort an Array](https://leetcode.com/problems/sort-an-array/) - Medium
- [Sort Colors](https://leetcode.com/problems/sort-colors/) - Medium
- [Insertion Sort List](https://leetcode.com/problems/insertion-sort-list/) - Medium
- [Kth Largest Element in an Array](https://leetcode.com/problems/kth-largest-element-in-an-array/) - Medium

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
