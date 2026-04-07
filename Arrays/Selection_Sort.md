---
created: 2026-04-07
revisions:
  - 2026-04-09
  - 2026-04-14
  - 2026-04-22
  - 2026-05-07
---

# Selection Sort

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Microsoft #Google #Apple #TCS #Infosys

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #sorting [[Sorting]], #arrays [[Arrays]], #greedy [[Greedy]]

## Pattern

Sorting (In-place) + Greedy Selection

---
## Difficulty

Easy
#easy

---

## ⚡ Key Idea (Core Insight)

Iteratively find the **minimum element** from the unsorted part of the array and swap it with the element at the beginning of the unsorted section.

---

## ⚡ Quick Recall (VERY IMPORTANT)

"Find min, swap with current start."
The sorted boundary grows by one element in each pass.

---

## Approach

### Brute Force
- Create a new array and repeatedly find/remove the minimum from the original.
- Time: O(N²) | Space: O(N)

### Better
- Selection Sort is already an "improvement" over Bubble Sort in terms of the number of swaps (O(N) swaps max).

### Optimal
- Maintain a pointer `i` for the boundary between sorted and unsorted parts.
- Find the index of the minimum element in range `[i, n-1]`.
- Swap `arr[i]` with `arr[min_index]`.
- Repeat for `i = 0` to `n-2`.

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

Input: `[29, 10, 14, 10, 37]` (Handling duplicates)

| Step | Current State | min_idx (Value) | Action |
| :--- | :--- | :--- | :--- |
| 1 | `[29, 10, 14, 10, 37]` | Index 1 (10) | Swap 29 with 10 (at index 1) |
| 2 | `[10, 29, 14, 10, 37]` | Index 3 (10) | Swap 29 with 10 (at index 3) |
| 3 | `[10, 10, 14, 29, 37]` | Index 2 (14) | 14 is already at index 2 (No swap) |
| 4 | `[10, 10, 14, 29, 37]` | Index 3 (29) | 29 is already at index 3 (No swap) |

---

## Edge Cases

- **Already Sorted:** `[1, 2, 3]` - Still performs O(N²) comparisons.
- **Reverse Sorted:** `[3, 2, 1]` - Maximum swaps and comparisons.
- **All Identical:** `[5, 5, 5]` - No swaps, but O(N²) comparisons.
- **Single Element:** `[1]` - Handled by loop range.
- **Negative Numbers:** `[-5, 2, -10]` - Logic holds for absolute values.

---

## Mistakes

- **Stability:** Not realizing Selection Sort is **not stable** (swaps can change relative order of duplicates).
- **Early Exit:** Trying to add an early break (unlike Bubble Sort, Selection Sort doesn't benefit from it).
- **User Mistake:** No specific note provided.

---

## Complexity

Time: O(N²) → Two nested loops to find the minimum for every position.  
Space: O(1) → In-place sorting, no extra data structures used.

---

## Similar Problems

- [Sort Colors](https://leetcode.com/problems/sort-colors/) - Medium
- [Kth Largest Element in an Array](https://leetcode.com/problems/kth-largest-element-in-an-array/) - Medium
- [Insertion Sort List](https://leetcode.com/problems/insertion-sort-list/) - Medium
- [Sort an Array](https://leetcode.com/problems/sort-an-array/) - Medium

---

## Tags and Properties
  - #dsa #important #revisit  
  - #sorting #selectionsort #easy_dsa
  - [[Sorting]] [[Array Patterns]]
  - Revision Date: 2026-04-07
  - **Problem Link:** [Selection Sort - GeeksforGeeks](https://www.geeksforgeeks.org/problems/selection-sort/1)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-09)
- [ ] Day 7 Revision (2026-04-14)
- [ ] Day 15 Revision (2026-04-22)
- [ ] Day 30 Revision (2026-05-07)
