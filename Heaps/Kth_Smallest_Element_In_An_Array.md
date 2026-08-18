---
created: 2026-08-19
revisions:
  - 2026-08-21
  - 2026-08-26
  - 2026-09-03
  - 2026-09-18
---

# Kth Smallest Element In An Array

---

## Metadata & Placement Tags

- **Target Companies:** #Amazon #Google #Microsoft #Facebook #Bloomberg
- **Confidence Checklist:**
  - [ ] Low
  - [ ] Medium
  - [ ] High
- **Concepts:** #heaps [[Heap]], #divideandconquer [[Divide and Conquer]], #sorting [[Sorting]]

---
## Pattern

Quickselect (Divide and Conquer) / Max-Heap

---
## Difficulty

Medium #medium

---
## ⚡ Key Idea (Core Insight)

Use Quickselect to partition the array around a random pivot, focusing only on the partition containing the target index `k-1` to achieve O(N) average time. Alternatively, maintain a Max-Heap of size `k` to track the `k` smallest elements encountered.

---
## ⚡ Quick Recall (VERY IMPORTANT)

Quickselect partitions recursively, discarding the half that does not contain index `k-1`. Max-heap tracks the smallest elements by popping the maximum when the size exceeds `k`.

---
## Approach

### Brute Force
Sort the array in ascending order and return the element at index `k-1`.
- **Time:** O(N log N)
- **Space:** O(1)

### Better
Maintain a Max-Heap of size `k`. Push elements into the heap. If the heap size exceeds `k`, pop the largest element.
- **Time:** O(N log k)
- **Space:** O(k)

### Optimal
**Optimal 1: Quickselect (Average O(N))**
1. Pick a random pivot.
2. Partition the array into elements smaller than the pivot and elements larger than the pivot.
3. If the pivot's final index is `k-1`, return it. Otherwise, recurse into the correct side.

**Optimal 2: Max-Heap (Python `heapq` simulation)**
Since Python only has a min-heap, push negative values (`-num`) to simulate a max-heap.

---
## Code (Python)

```python
import random
import heapq

class Solution:
    def findKthSmallestQuickselect(self, nums: list[int], k: int) -> int:
        def select(left: int, right: int, k_smallest: int) -> int:
            if left == right:
                return nums[left]

            # Random pivot to avoid O(N^2) worst-case on sorted input
            pivot_idx = random.randint(left, right)
            nums[pivot_idx], nums[right] = nums[right], nums[pivot_idx]

            pivot = nums[right]
            i = left
            for j in range(left, right):
                if nums[j] < pivot:
                    nums[i], nums[j] = nums[j], nums[i]
                    i += 1
            nums[i], nums[right] = nums[right], nums[i]

            if i == k_smallest:
                return nums[i]
            elif i < k_smallest:
                return select(i + 1, right, k_smallest)
            else:
                return select(left, i - 1, k_smallest)

        return select(0, len(nums) - 1, k - 1)

    def findKthSmallestMaxHeap(self, nums: list[int], k: int) -> int:
        max_heap = []
        for num in nums:
            # Simulate max heap by negating numbers
            heapq.heappush(max_heap, -num)
            if len(max_heap) > k:
                heapq.heappop(max_heap)
        return -max_heap[0]
```

---
## Dry Run (Smart Example)

Input: `nums = [3, -2, 5, 0]`, `k = 2` (Max-Heap Approach)

| Step | Variables | Explanation |
| :--- | :--- | :--- |
| 1 | `num = 3`, `max_heap = [-3]` | Push `-3`. Size (1) <= 2. |
| 2 | `num = -2`, `max_heap = [-3, 2]` | Push `2` (negative of `-2`). Size (2) <= 2. |
| 3 | `num = 5`, `max_heap = [2, -3, -5]` | Push `-5`. Size (3) > 2. Pop max element `2` from heap. Heap becomes `[-3, -5]`. |
| 4 | `num = 0`, `max_heap = [0, -3, -5]` | Push `0`. Size (3) > 2. Pop max element `0` from heap. Heap becomes `[-3, -5]`. |
| End | Return `-max_heap[0]` -> `0` | Root is `0` (or `-0`). Negating gives `0`. Correct 2nd smallest element. |

---
## Edge Cases

- **`k = 1` or `k = len(nums)`**: Finding the absolute minimum or maximum element.
- **Negative numbers**: Ensure negated signs do not break heap ordering and are correctly double-negated when retrieved.
- **Duplicates**: Quickselect partition pointers must handle equal values without infinite loops.

---
## Mistakes

- **Incorrect Min/Max Simulation**: Forgetting to negate the retrieved value when returning `-max_heap[0]`, resulting in negative outputs.
- **Determinism in Quickselect**: Using a fixed pivot (like the first/last element), triggering $O(N^2)$ time on pre-sorted arrays.
- **Off-by-One**: Confusing 1-based `k` with 0-based indexing (`k - 1`) during partitioning checks.

---
## Complexity

### Quickselect
- **Time:** O(N) average, O(N^2) worst-case.
- **Space:** O(1) auxiliary (ignoring recursion stack).

### Max-Heap
- **Time:** O(N log k)
- **Space:** O(k)

---
## Similar Problems

- [Kth Largest Element in an Array](https://leetcode.com/problems/kth-largest-element-in-an-array/) - Medium
- [Top K Frequent Elements](https://leetcode.com/problems/top-k-frequent-elements/) - Medium
- [K Closest Points to Origin](https://leetcode.com/problems/k-closest-points-to-origin/) - Medium

---
## Tags and Properties

- #dsa #important #revisit #heaps #quickselect
- Obsidian Links: [[Heap]], [[Divide and Conquer]], [[Sorting]]
- Revision Date: 2026-08-19
- **Problem Link:** [LeetCode - Kth Largest Element in an Array](https://leetcode.com/problems/kth-largest-element-in-an-array/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-08-21)
- [ ] Day 7 Revision (2026-08-26)
- [ ] Day 15 Revision (2026-09-03)
- [ ] Day 30 Revision (2026-09-18)
