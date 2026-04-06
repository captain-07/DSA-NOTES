---
created: 2026-04-06
revisions:
  - 2026-04-08
  - 2026-04-13
  - 2026-04-21
  - 2026-05-06
---

# Selection Sort

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Microsoft #TCS #Infosys #GoldmanSachs

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #sorting [[Sorting]] #arrays [[Arrays]] #greedy [[Greedy]]

## Pattern

In-place Comparison + Minimum Selection

---
## Difficulty

Easy
#easy

---

## ⚡ Key Idea (Core Insight)

Maintain two parts in the array: a **sorted** subarray and an **unsorted** subarray. In every iteration, find the **minimum** element from the unsorted part and swap it with the first element of the unsorted part, effectively "growing" the sorted section by one.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Find the smallest, swap to the front, move the boundary. Repeat $N-1$ times.

---

## Approach

### Brute Force / Optimal
Selection Sort consistently performs $O(n^2)$ comparisons regardless of the initial order of elements. There is no significantly "better" version of this specific algorithm, though Heap Sort is its $O(n \log n)$ evolution.

**Optimal Logic:**
1. Loop $i$ from $0$ to $n-1$ (this is the boundary).
2. Assume `i` is the index of the minimum element (`min_idx = i`).
3. Loop $j$ from $i+1$ to $n-1$ to find the actual minimum in the remaining part.
4. After the inner loop, swap `arr[i]` with `arr[min_idx]`.
5. Repeat until the boundary reaches the end.

---

## Code (Python)

```python
def selection_sort(arr):
    n = len(arr)
    # Traverse through all array elements
    for i in range(n):
        # Find the minimum element in remaining unsorted array
        min_idx = i
        for j in range(i + 1, n):
            if arr[j] < arr[min_idx]:
                min_idx = j
                
        # Swap the found minimum element with the first element
        arr[i], arr[min_idx] = arr[min_idx], arr[i]
    return arr
```

---

## Dry Run (Smart Example)

Input: `[29, 10, 14, 37, 14]` (Contains duplicates)

| Step | Current `i` | `min_idx` found | Array after Swap | Explanation |
| :--- | :--- | :--- | :--- | :--- |
| 1 | 0 (val 29) | 1 (val 10) | `[10, 29, 14, 37, 14]` | 10 is smallest; swap with index 0. |
| 2 | 1 (val 29) | 2 (val 14) | `[10, 14, 29, 37, 14]` | 14 is smallest in [29, 14, 37, 14]. |
| 3 | 2 (val 29) | 4 (val 14) | `[10, 14, 14, 37, 29]` | Second 14 found at index 4; swap with 29. |
| 4 | 3 (val 37) | 4 (val 29) | `[10, 14, 14, 29, 37]` | 29 is smaller than 37; swap. |

---

## Edge Cases

- **Empty Array:** Loop doesn't execute; returns empty list.
- **Already Sorted:** Still performs $O(n^2)$ comparisons (not adaptive).
- **Reverse Sorted:** Maximum number of swaps/comparisons.
- **Duplicate Elements:** Handles them normally, but the algorithm is **unstable** (relative order of 14s might change).

---

## Mistakes

- **Stability:** Forgetting that Selection Sort is typically NOT stable (swapping can jump elements over others).
- **Redundant Swaps:** Swapping even if `min_idx == i` (can add a check, though usually omitted for brevity).
- **User Mistake:** No specific note provided.

---

## Complexity

Time: O($N^2$) → Nested loops (N + N-1 + N-2... + 1) result in quadratic time.  
Space: O(1) → Performed in-place without auxiliary data structures.

---

## Tags and Properties

- #dsa #important #revisit #sorting #inplace
- [[Sorting]] [[Array Manipulation]]
- Revision Date: 2026-04-06
- Related: [[Bubble Sort]], [[Insertion Sort]]

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-08)
- [ ] Day 7 Revision (2026-04-13)
- [ ] Day 15 Revision (2026-04-21)
- [ ] Day 30 Revision (2026-05-06)
