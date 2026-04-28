---
created: 2026-04-10
revisions:
  - 2026-04-12
  - 2026-04-17
  - 2026-04-25
  - 2026-05-10
---

# Selection Sort

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Microsoft #GoldmanSachs #TCS #Infosys

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #sorting [[Sorting]], #arrays [[Arrays]], #greedy [[Greedy]]

## Pattern

In-place Sorting + Incremental Building

---
## Difficulty

Easy
#easy

---

## ⚡ Key Idea (Core Insight)

Divide the array into a sorted and unsorted part. In each iteration, find the **minimum element** from the unsorted part and swap it with the first element of that unsorted section.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Repeatedly pick the **smallest** remaining element and move it to its correct position at the front.

---

## Approach

### Brute Force
- Standard Selection Sort is already $O(n^2)$.
- Time Complexity: $O(n^2)$
- Space Complexity: $O(1)$

### Optimal
1. Iterate from $i = 0$ to $n-2$.
2. Assume $i$ is the `min_index`.
3. Scan the rest of the array ($j = i+1$ to $n-1$) to find the actual minimum element's index.
4. Swap the element at `min_index` with the element at $i$.
5. Repeat until the entire array is sorted.

---

## Code (Python)

```python
class Solution:
    def selectionSort(self, arr: list[int]) -> list[int]:
        """
        Standard Selection Sort implementation.
        Finds the minimum in each pass and swaps it to the front.
        """
        n = len(arr)
        
        for i in range(n - 1):
            # Assume the current position is the minimum
            min_idx = i
            
            # Find the actual minimum in the unsorted portion
            for j in range(i + 1, n):
                if arr[j] < arr[min_idx]:
                    min_idx = j
            
            # Swap the found minimum with the first element of unsorted part
            if min_idx != i:
                arr[i], arr[min_idx] = arr[min_idx], arr[i]
                
        return arr
```

---

## Dry Run (Smart Example)

**Input:** `[5, 2, 8, 2, 1]` (Contains duplicates)

| Step | Variables (i, min_idx) | Array State | Explanation |
| :--- | :--- | :--- | :--- |
| 0 | Start | `[5, 2, 8, 2, 1]` | Initial unsorted array. |
| 1 | i=0, min_idx=4 | `[1, 2, 8, 2, 5]` | Found '1' at index 4; swapped with index 0. |
| 2 | i=1, min_idx=1 | `[1, 2, 8, 2, 5]` | Found '2' at index 1; no swap needed (or swap with self). |
| 3 | i=2, min_idx=3 | `[1, 2, 2, 8, 5]` | Found '2' at index 3; swapped with index 2. |
| 4 | i=3, min_idx=4 | `[1, 2, 2, 5, 8]` | Found '5' at index 4; swapped with index 3. |

---

## Edge Cases

- **Already Sorted:** `[1, 2, 3, 4, 5]` - Still performs $O(n^2)$ comparisons.
- **Reverse Sorted:** `[5, 4, 3, 2, 1]` - Maximum number of swaps.
- **All Elements Same:** `[2, 2, 2]` - Handled correctly, no swaps performed if optimized.
- **Empty or Single Element:** `[]` or `[1]` - Loop constraints handle this automatically.

---

## Mistakes

- **Not Stable:** Selection Sort is not stable by default (swapping can change the relative order of equal elements).
- **Inefficiency:** It always takes $O(n^2)$ time even if the array is sorted (unlike Bubble Sort with a flag).
- **User Mistake:** No specific note provided.

---

## Complexity

**Time: $O(n^2)$** → Two nested loops: $(n-1) + (n-2) + ... + 1$ comparisons.  
**Space: $O(1)$** → Only uses a few variables for indices; sorting is done in-place.

---

## Similar Problems

- [Bubble Sort](https://www.geeksforgeeks.org/bubble-sort/) - Easy
- [Insertion Sort](https://leetcode.com/problems/insertion-sort-list/) - Easy
- [Kth Largest Element in an Array](https://leetcode.com/problems/kth-largest-element-in-an-array/) - Medium (Can use Selection Sort logic/QuickSelect)

---

## Tags and Properties
  - #dsa #important #revisit #sorting  
  - [[Sorting]] [[Arrays]] [[Greedy]]
  - **Revision Date:** 2026-04-10
  - **Problem Link:** [Selection Sort - GeeksforGeeks](https://www.geeksforgeeks.org/problems/selection-sort/1)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-12)
- [ ] Day 7 Revision (2026-04-17)
- [ ] Day 15 Revision (2026-04-25)
- [ ] Day 30 Revision (2026-05-10)
