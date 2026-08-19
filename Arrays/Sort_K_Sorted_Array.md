---
created: 2026-08-20
revisions:
  - 2026-08-22
  - 2026-08-27
  - 2026-09-04
  - 2026-09-19
---

# Sort K Sorted Array

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Google #Microsoft #Uber #Flipkart

- **Confidence Checklist:**
  - [ ] Low
  - [ ] Medium
  - [ ] High

- **Concepts:**
  - #heap [[Heap]]
  - #sorting [[Sorting]]

## Pattern

- Heap / Priority Queue (Sliding Window Heap)

---
## Difficulty

Medium
#medium

---
## ⚡ Key Idea (Core Insight)

Since each element is at most $k$ positions away from its sorted index, the minimum element for any index $i$ must reside within the range $[i, i + k]$. A min-heap of size $k + 1$ maintains this sliding window of candidates, allowing us to find the correct minimum element for each index in $O(\log k)$ time.

---
## ⚡ Quick Recall (VERY IMPORTANT)

Maintain a min-heap of size $k+1$. Pop the minimum to the current write position, then push the next element from the array.

---
## Approach

### Brute Force
- Sort the entire array.
- Time Complexity: $O(N \log N)$

### Optimal
- Initialize a min-heap with the first $k + 1$ elements of the array.
- Iterate from index $k + 1$ to $N - 1$:
  - Pop the smallest element from the heap and write it to `arr[write_idx]`.
  - Push the current element `arr[read_idx]` into the heap.
  - Increment `write_idx`.
- Empty the remaining elements from the heap into the rest of the array.

---
## Code (Python)

```python
import heapq

class Solution:
    def sortKSortedArray(self, arr: list[int], k: int) -> list[int]:
        n = len(arr)
        # Create a min-heap with the first k + 1 elements
        heap = arr[:k + 1]
        heapq.heapify(heap)

        write_idx = 0
        # Process remaining elements using heappushpop
        for read_idx in range(k + 1, n):
            arr[write_idx] = heapq.heappushpop(heap, arr[read_idx])
            write_idx += 1

        # Empty the remaining elements from the heap
        while heap:
            arr[write_idx] = heapq.heappop(heap)
            write_idx += 1

        return arr
```

---
## Dry Run (Smart Example)

Input: `arr = [3, -1, 2, 6, 8, 4]`, `k = 2`

| Step | Variables | Explanation |
| :--- | :--- | :--- |
| Init | `heap=[-1, 3, 2]`, `write_idx=0` | Heapify first `k + 1 = 3` elements `[3, -1, 2]`. |
| 1 | `read_idx=3` (val `6`), `write_idx=1` | `heappushpop(6)` pops `-1` to `arr[0]`. Heap: `[2, 3, 6]`. |
| 2 | `read_idx=4` (val `8`), `write_idx=2` | `heappushpop(8)` pops `2` to `arr[1]`. Heap: `[3, 8, 6]`. |
| 3 | `read_idx=5` (val `4`), `write_idx=3` | `heappushpop(4)` pops `3` to `arr[2]`. Heap: `[4, 8, 6]`. |
| 4 | `write_idx=6` | Pop remaining elements `[4, 6, 8]` to `arr[3..5]`. Final: `[-1, 2, 3, 4, 6, 8]`. |

---
## Edge Cases

- `k = 0`: Array is already sorted; heap size is 1, elements are written back immediately.
- `k >= len(arr)`: Heap stores all elements; acts as a standard heap sort.
- Duplicates/Negatives: Correctly handled by standard min-heap ordering properties.

---
## Mistakes

- **Using a write index to modify the arr in place prematurely**: Overwriting elements in `arr` before they have been read or pushed into the heap. (Avoided by pre-populating the heap with $k + 1$ elements before writing to index `0`).
- Using a heap of size $k$ instead of $k + 1$, which misses the boundary candidate.

---
## Complexity

Time: O($N \log k$) → Each of the $N$ elements is pushed and popped from a heap of size $k+1$.
Space: O($k$) → The min-heap stores at most $k + 1$ elements.

---
## Similar Problems

- [Merge k Sorted Lists](https://leetcode.com/problems/merge-k-sorted-lists/) - Hard
- [Find K Closest Elements](https://leetcode.com/problems/find-k-closest-elements/) - Medium
- [Top K Frequent Elements](https://leetcode.com/problems/top-k-frequent-elements/) - Medium
- [Kth Largest Element in an Array](https://leetcode.com/problems/kth-largest-element-in-an-array/) - Medium

---
## Tags and Properties

- #dsa #important #revisit #heap #sorting [[Heap]] [[Sorting]]
- Revision Date: 2026-08-20
- **Problem Link:** [GeeksforGeeks - Nearly Sorted](https://www.geeksforgeeks.org/problems/nearly-sorted-1587115620/1)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-08-22)
- [ ] Day 7 Revision (2026-08-27)
- [ ] Day 15 Revision (2026-09-04)
- [ ] Day 30 Revision (2026-09-19)
