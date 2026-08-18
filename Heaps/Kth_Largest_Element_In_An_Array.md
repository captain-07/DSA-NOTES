---
created: 2026-08-18
revisions:
  - 2026-08-20
  - 2026-08-25
  - 2026-09-02
  - 2026-09-17
---

# Kth Largest Element In An Array

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Google #Microsoft #Facebook
- **Confidence Checklist:**
  - [ ] Low
  - [ ] Medium
  - [ ] High
- **Concepts:**
  - #heap [[Heap]], #divideandconquer [[Divide and Conquer]], #sorting [[Sorting]]

## Pattern
Heap (Min-Heap) + Quickselect

---
## Difficulty
Medium
#medium

---
## ⚡ Key Idea (Core Insight)
Maintain a min-heap of size `k` to keep track of the `k` largest elements seen so far; the root will hold the kth largest element. Alternatively, partition the array using Quickselect to locate the target index `n - k` in average $O(n)$ time.

---
## ⚡ Quick Recall (VERY IMPORTANT)
Min-heap of size `k` maintains the `k` largest elements at the top. Quickselect partitions around a random pivot to target index `n - k`.

---
## Approach

### Brute Force
Sort the array in descending order and return the element at index `k - 1`.
Time: $O(n \log n)$ | Space: $O(1)$

### Optimal 1: Min-Heap
1. Initialize a min-heap.
2. Push elements from the array into the heap.
3. If heap size exceeds `k`, pop the smallest element.
4. Return the root element of the heap.

### Optimal 2: Quickselect (Average O(n))
1. Set target index to `len(nums) - k`.
2. Partition the array around a randomly selected pivot.
3. If pivot's final index equals the target index, return the pivot value.
4. Otherwise, recursively partition only the left or right subarray containing the target index.

---
## Code (Python)

```python
import heapq
import random

class Solution:
    # Option 1: Min-Heap Approach
    def findKthLargest_heap(self, nums: list[int], k: int) -> int:
        min_heap = []
        for num in nums:
            heapq.heappush(min_heap, num)
            if len(min_heap) > k:
                heapq.heappop(min_heap)
        return min_heap[0]

    # Option 2: Quickselect Approach
    def findKthLargest_quickselect(self, nums: list[int], k: int) -> int:
        target = len(nums) - k

        def quickselect(left: int, right: int) -> int:
            pivot_idx = random.randint(left, right)
            pivot = nums[pivot_idx]
            nums[pivot_idx], nums[right] = nums[right], nums[pivot_idx]

            store_idx = left
            for i in range(left, right):
                if nums[i] < pivot:
                    nums[store_idx], nums[i] = nums[i], nums[store_idx]
                    store_idx += 1

            nums[store_idx], nums[right] = nums[right], nums[store_idx]

            if store_idx == target:
                return nums[store_idx]
            elif store_idx < target:
                return quickselect(store_idx + 1, right)
            else:
                return quickselect(left, store_idx - 1)

        return quickselect(0, len(nums) - 1)
```

---
## Dry Run (Smart Example)

Input: `nums = [3, 2, -1, 5, 4, 3]`, `k = 3` (Expected: `3`)

| Step | Variables | Explanation |
| :--- | :--- | :--- |
| 1 | `num = 3`, `heap = [3]` | Push `3`. Size <= 3. |
| 2 | `num = 2`, `heap = [2, 3]` | Push `2`. Size <= 3. |
| 3 | `num = -1`, `heap = [-1, 3, 2]` | Push `-1`. Size <= 3. |
| 4 | `num = 5`, `heap = [2, 3, 5]` | Push `5`, pop root `-1`. |
| 5 | `num = 4`, `heap = [3, 4, 5]` | Push `4`, pop root `2`. |
| 6 | `num = 3`, `heap = [3, 4, 5]` | Push `3`, pop root `3`. |
| End | `heap[0] = 3` | Return heap root. |

---
## Edge Cases

- **$k = 1$ or $k = n$**: Boundaries of the array (maximum/minimum values).
- **All duplicates (e.g., `[5, 5, 5, 5]`)**: Algorithm must correctly handle redundant swaps or values.
- **Negative numbers (e.g., `[-3, -1, -2]`, `k = 2`)**: Sorting order of negative values must remain correct.

---
## Mistakes

- Solving this using a min heap is more intuitive than solving using quickselect, but Quickselect has better average time complexity.
- Off-by-one errors when translating the $k$-th largest element to index `n - k`.
- Not choosing a random pivot in Quickselect, resulting in worst-case $O(n^2)$ complexity on sorted inputs.

---
## Complexity

### Min-Heap
- **Time:** $O(n \log k)$ → Iterates through $n$ elements, maintaining a heap of size $k$.
- **Space:** $O(k)$ → Stores at most $k$ elements in memory.

### Quickselect
- **Time:** $O(n)$ average, $O(n^2)$ worst-case → Average reduction of search space by half each step.
- **Space:** $O(1)$ → Iterative approach requires no extra stack space.

---
## Similar Problems

- [K Closest Points to Origin](https://leetcode.com/problems/k-closest-points-to-origin/) - Medium
- [Top K Frequent Elements](https://leetcode.com/problems/top-k-frequent-elements/) - Medium
- [Find Median from Data Stream](https://leetcode.com/problems/find-median-from-data-stream/) - Hard

---
## Tags and Properties
- #dsa #important #revisit #heap #quickselect
- Obsidian links: [[Heap]] [[Divide and Conquer]] [[Sorting]]
- Revision Date: 2026-08-18
- **Problem Link:** [LeetCode - Kth Largest Element in an Array](https://leetcode.com/problems/kth-largest-element-in-an-array/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-08-20)
- [ ] Day 7 Revision (2026-08-25)
- [ ] Day 15 Revision (2026-09-02)
- [ ] Day 30 Revision (2026-09-17)
