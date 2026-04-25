---
created: 2026-04-25
revisions:
  - 2026-04-27
  - 2026-05-02
  - 2026-05-10
  - 2026-05-25
---

# Merge Two Sorted Arrays Without Extra Space

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Microsoft #GoldmanSachs #Adobe #LinkedIn

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #sorting [[Sorting]], #twopointers [[Two Pointers]], #shellsort [[Gap Method]]

---
## Pattern

Two Pointers + Insertion  
Gap Method (Shell Sort based)

---
## Difficulty

Hard  
#hard

---

## ⚡ Key Idea (Core Insight)

The challenge is the $O(1)$ space constraint. Instead of merging into a new array, use the **Gap Method** (derived from Shell Sort). By comparing elements at a specific "gap" across both arrays and swapping if they are out of order, the arrays eventually become fully sorted without extra memory.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Gap = `ceil((n+m)/2)`. Iterate with `i` and `j = i + gap`. Swap if `arr[i] > arr[j]`. Reduce gap by half (`gap/2`) until gap = 0.

---

## Approach

### Brute Force
- Create a third array of size $n+m$, copy all elements, sort it, and copy back.
- Time: $O((n+m) \log(n+m))$ | Space: $O(n+m)$

### Better (Two Pointers + Sorting)
- Compare the end of `arr1` with the start of `arr2`. 
- If `arr1[i] > arr2[j]`, swap them and move pointers.
- Finally, sort both arrays individually.
- Time: $O(n \log n + m \log m)$ | Space: $O(1)$

### Optimal (Gap Method)
1. Initialize `gap = ceil((n + m) / 2)`.
2. Use two pointers `left` and `right` (where `right = left + gap`).
3. Iterate through the virtual combined array. If `arr[left] > arr[right]`, swap.
4. If `right` reaches the end, reduce `gap = ceil(gap / 2)`.
5. Repeat until `gap < 1`.

---

## Code (Python)

```python
import math

class Solution:
    def merge(self, arr1, arr2, n, m):
        # Initial gap calculation
        total_len = n + m
        gap = math.ceil(total_len / 2)
        
        while gap > 0:
            left = 0
            right = left + gap
            
            while right < total_len:
                # Case 1: Both pointers in arr1
                if left < n and right < n:
                    if arr1[left] > arr1[right]:
                        arr1[left], arr1[right] = arr1[right], arr1[left]
                # Case 2: Left in arr1, Right in arr2
                elif left < n and right >= n:
                    if arr1[left] > arr2[right - n]:
                        arr1[left], arr2[right - n] = arr2[right - n], arr1[left]
                # Case 3: Both pointers in arr2
                else:
                    if arr2[left - n] > arr2[right - n]:
                        arr2[left - n], arr2[right - n] = arr2[right - n], arr2[left - n]
                
                left += 1
                right += 1
            
            if gap == 1: break
            gap = math.ceil(gap / 2)
```

---

## Dry Run (Smart Example)

**Input:** `arr1 = [1, 5, 9]`, `arr2 = [2, 3]`, `n=3, m=2`. Total length = 5.

| Step | Gap | Pointers (L, R) | Comparison | Action | Result |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | 3 | L=0, R=3 | arr1[0] vs arr2[0] (1 vs 2) | No Swap | [1, 5, 9], [2, 3] |
| 2 | 3 | L=1, R=4 | arr1[1] vs arr2[1] (5 vs 3) | **Swap** | [1, 3, 9], [2, 5] |
| 3 | 2 | L=0, R=2 | arr1[0] vs arr1[2] (1 vs 9) | No Swap | [1, 3, 9], [2, 5] |
| 4 | 2 | L=1, R=3 | arr1[1] vs arr2[0] (3 vs 2) | **Swap** | [1, 2, 9], [3, 5] |
| 5 | 1 | L=2, R=3 | arr1[2] vs arr2[0] (9 vs 3) | **Swap** | [1, 2, 3], [9, 5] |
| 6 | 1 | L=3, R=4 | arr2[0] vs arr2[1] (9 vs 5) | **Swap** | [1, 2, 3], [5, 9] |

---

## Edge Cases

- **One array is empty:** Gap logic still holds (total length = $n$ or $m$).
- **Arrays already sorted:** O(N) comparisons per gap level, no swaps.
- **Identical elements:** Swaps are skipped, maintaining stability isn't guaranteed (but not required).
- **Large Gap:** Ensure `math.ceil` is used to avoid infinite loops on `gap=1`.

---

## Mistakes

- **User mistake:** No specific note provided.
- **Incorrect pointer indexing:** Forgetting to subtract `n` from `right` or `left` when accessing `arr2`.
- **Gap reduction:** Using `gap // 2` instead of `ceil(gap / 2)` can cause the gap to skip `1`.
- **Termination:** Ending the loop before `gap = 1` is fully processed.

---

## Complexity

Time: $O((n + m) \log(n + m))$ → Logarithmic gap reductions, each taking linear time.  
Space: $O(1)$ → All swaps are done in-place.

---

## Similar Problems

- [Merge Sorted Array (LeetCode 88)](https://leetcode.com/problems/merge-sorted-array/) - Easy
- [Merge Intervals](https://leetcode.com/problems/merge-intervals/) - Medium
- [Median of Two Sorted Arrays](https://leetcode.com/problems/median-of-two-sorted-arrays/) - Hard

---

## Tags and Properties
- #dsa #important #revisit  
- #arrays #inplace #sorting  
- [[Gap Method]] [[Two Pointers]]
- **Revision Date:** 2026-04-25
- **Problem Link:** [GeeksforGeeks - Merge Without Extra Space](https://www.geeksforgeeks.org/problems/merge-two-sorted-arrays-1587115620/1)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-27)
- [ ] Day 7 Revision (2026-05-02)
- [ ] Day 15 Revision (2026-05-10)
- [ ] Day 30 Revision (2026-05-25)
