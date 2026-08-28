---
created: 2026-08-28
revisions:
  - 2026-08-30
  - 2026-09-04
  - 2026-09-12
  - 2026-09-27
---

# Merge K Sorted Lists

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Google #Microsoft #Facebook #Bloomberg
- **Confidence Checklist:**
  - [ ] Low
  - [ ] Medium
  - [ ] High
- **Concepts:**
  - #heaps [[Heap/Priority Queue]]
  - #divideandconquer [[Divide and Conquer]]
  - #linkedlist [[Linked List]]

---
## Pattern

Heap (Priority Queue) / Divide and Conquer (Merge Sort style)

---
## Difficulty

Hard
#hard

---
## ⚡ Key Idea (Core Insight)

To efficiently merge $K$ sorted lists, continuously retrieve the smallest element among the current heads of the lists. This can be done using a Min-Heap of size $K$, or by merging the lists pairwise using a divide-and-conquer approach.

---
## ⚡ Quick Recall (VERY IMPORTANT)

Use a Min-Heap containing the tuple `(val, index, node)` for the head of each list, or merge lists pairwise (Divide & Conquer) to reduce $K$ to $1$ in $O(\log K)$ passes.

---
## Approach

### Brute Force
- Traverse all lists, store all node values in an array, sort the array, and build a new sorted linked list.
- Time: $O(N \log N)$ where $N$ is the total number of nodes.
- Space: $O(N)$

### Optimal 1: Min-Heap (Priority Queue)
- Insert the head of each non-empty list into a Min-Heap.
- Extract the minimum node, append it to the result list, and insert the next node from that same list into the heap.
- Repeat until the heap is empty.
- Time: $O(N \log K)$
- Space: $O(K)$

### Optimal 2: Divide & Conquer
- Pairwise merge lists: merge list $i$ and $i+1$, reducing the number of lists by half each time.
- Repeat until only one merged list remains.
- Time: $O(N \log K)$
- Space: $O(1)$ iterative / $O(\log K)$ recursive stack

---
## Code (Python)

```python
import heapq

# Definition for singly-linked list.
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

class Solution:
    # --- Option 1: Min-Heap Approach ---
    def mergeKListsHeap(self, lists: list[ListNode]) -> ListNode:
        heap = []
        # Push the head of each list with a unique index to prevent node comparison errors
        for i, l in enumerate(lists):
            if l:
                heapq.heappush(heap, (l.val, i, l))

        dummy = ListNode(0)
        curr = dummy

        while heap:
            val, i, node = heapq.heappop(heap)
            curr.next = node
            curr = curr.next
            if node.next:
                heapq.heappush(heap, (node.next.val, i, node.next))

        return dummy.next

    # --- Option 2: Divide & Conquer Approach ---
    def mergeKLists(self, lists: list[ListNode]) -> ListNode:
        if not lists:
            return None

        def mergeTwo(l1, l2):
            dummy = ListNode(0)
            curr = dummy
            while l1 and l2:
                if l1.val < l2.val:
                    curr.next, l1 = l1, l1.next
                else:
                    curr.next, l2 = l2, l2.next
                curr = curr.next
            curr.next = l1 or l2
            return dummy.next

        interval = 1
        n = len(lists)
        while interval < n:
            for i in range(0, n - interval, interval * 2):
                lists[i] = mergeTwo(lists[i], lists[i + interval])
            interval *= 2

        return lists[0]
```

---
## Dry Run (Smart Example)

Input: `lists = [[1, 4], [1, 3], [2, 6]]`

| Step | Heap State (val, list_idx, node) | Action / Variables | Explanation |
| :--- | :--- | :--- | :--- |
| **0** | `[(1, 0, n_1a), (1, 1, n_2a), (2, 2, n_3a)]` | Initialize heap | Push heads `1` (from L0), `1` (from L1), `2` (from L2). Dummy points to empty. |
| **1** | `[(1, 1, n_2a), (2, 2, n_3a), (4, 0, n_1b)]` | Pop `(1, 0, n_1a)`. Push L0 next `4`. | `curr.next` links to `1` (L0). Heap gets `4` from L0. |
| **2** | `[(2, 2, n_3a), (4, 0, n_1b), (3, 1, n_2b)]` | Pop `(1, 1, n_2a)`. Push L1 next `3`. | `curr.next` links to `1` (L1). Heap gets `3` from L1. |
| **3** | `[(3, 1, n_2b), (4, 0, n_1b), (6, 2, n_3b)]` | Pop `(2, 2, n_3a)`. Push L2 next `6`. | `curr.next` links to `2` (L2). Heap gets `6` from L2. |

---
## Edge Cases

- `lists = []` -> Return `None` immediately.
- `lists = [[]]` or `[[], []]` -> Return `None` (handled by skipping empty lists in heap setup).
- `k = 1` -> Return `lists[0]` directly.
- Single node lists e.g., `[[1], [0], [-1]]` -> Negative values are handled properly by the Min-Heap.

---
## Mistakes

- No specific note provided.
- Comparing `ListNode` objects directly in Python's `heapq` (causes `TypeError`). Always insert a unique index or counter as the second tuple element to break ties.
- Forgetting to update the list pointer (`node = node.next`) before pushing the next element back into the heap.

---
## Complexity

Time: $O(N \log K)$ → Total $N$ nodes are pushed and popped from the heap. Each heap operation takes $O(\log K)$ time.
Space: $O(K)$ → The heap stores at most $K$ nodes (one from each list) at any given time.

---
## Similar Problems

- [Merge Two Sorted Lists](https://leetcode.com/problems/merge-two-sorted-lists/) - Easy
- [Kth Smallest Element in a Sorted Matrix](https://leetcode.com/problems/kth-smallest-element-in-a-sorted-matrix/) - Medium
- [Ugly Number II](https://leetcode.com/problems/ugly-number-ii/) - Medium

---
## Tags and Properties

- #dsa #important #revisit #heaps #linkedlist #divideandconquer
- [[Heap/Priority Queue]] [[Divide and Conquer]] [[Linked List]]
- **Revision Date:** 2026-08-28
- **Problem Link:** [LeetCode - Merge k Sorted Lists](https://leetcode.com/problems/merge-k-sorted-lists/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-08-30)
- [ ] Day 7 Revision (2026-09-04)
- [ ] Day 15 Revision (2026-09-12)
- [ ] Day 30 Revision (2026-09-27)
