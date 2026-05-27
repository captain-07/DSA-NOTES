---
created: 2026-05-18
revisions:
  - 2026-05-20
  - 2026-05-25
  - 2026-06-02
  - 2026-06-17
---

# Sort LL

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Microsoft #Google #Adobe #Facebook #ByteDance

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #linkedlist [[Linked List]]
  - #sorting [[Sorting]]
  - #divideandconquer [[Divide and Conquer]]
  - #twopointers [[Two Pointers]]

---
## Pattern

Divide and Conquer (Merge Sort) + Two Pointers (Slow/Fast)

---
## Difficulty

Medium  
#medium

---

## ⚡ Key Idea (Core Insight)

Use **Merge Sort** to achieve $O(n \log n)$ time. Since random access is impossible in Linked Lists, Quick Sort is inefficient. Split the list into two halves using the **Fast and Slow pointer** technique, recursively sort them, and merge using the "Merge Two Sorted Lists" logic.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Split with Slow/Fast (remember to break the link!) → Recursively Sort → Merge sorted halves.

---

## Approach

### Brute Force
- Copy all node values into an array, sort the array ($O(n \log n)$), and rewrite values back into nodes.
- **Time:** $O(n \log n)$
- **Space:** $O(n)$ extra space for the array.

### Optimal (Merge Sort)
1. **Base Case:** If `head` is `None` or `head.next` is `None`, return `head`.
2. **Split:** Find the middle using Slow/Fast pointers. Crucially, set `slow.next = None` to disconnect the two halves.
3. **Recurse:** Call `sortList` on the left and right heads.
4. **Merge:** Combine the two sorted halves into one sorted list.

---

## Code (Python)

```python
class Solution:
    def sortList(self, head: Optional[ListNode]) -> Optional[ListNode]:
        if not head or not head.next:
            return head
        
        # 1. Split the list into two halves
        mid = self.get_mid(head)
        left = head
        right = mid.next
        mid.next = None # Break the link
        
        # 2. Recursively sort
        left_sorted = self.sortList(left)
        right_sorted = self.sortList(right)
        
        # 3. Merge sorted halves
        return self.merge(left_sorted, right_sorted)

    def get_mid(self, head):
        slow, fast = head, head.next
        while fast and fast.next:
            slow = slow.next
            fast = fast.next.next
        return slow

    def merge(self, l1, l2):
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
```

---

## Dry Run (Smart Example)

**Input:** `[4, 2, 1, 3]`

| Step | Variables | Explanation |
| :--- | :--- | :--- |
| 1 | `head=[4,2,1,3]` | `get_mid` finds `2`. Split into `[4,2]` and `[1,3]`. |
| 2 | `left=[4,2]` | Split into `[4]` and `[2]`. Base case reached. Merge → `[2,4]`. |
| 3 | `right=[1,3]` | Split into `[1]` and `[3]`. Base case reached. Merge → `[1,3]`. |
| 4 | `merge([2,4], [1,3])` | Compare 2 vs 1 → 1; 2 vs 3 → 2; 4 vs 3 → 3; append 4. Result: `[1,2,3,4]`. |

---

## Edge Cases

- **Empty List (`None`):** Handled by base case; returns `None`.
- **Single Node:** Handled by base case; returns node.
- **Already Sorted:** Logic remains the same, still $O(n \log n)$.
- **Reverse Sorted / Duplicates:** Merge logic handles these correctly.

---

## Mistakes

- **Forgetting to break the link:** If you don't set `mid.next = None`, you get infinite recursion.
- **Finding the wrong mid:** For even-length lists, `fast = head.next` ensures `slow` stops at the "end of the first half" rather than the "start of the second half".
- **User Mistake:** Attempting Quick Sort on a Linked List is harder because you can't efficiently swap elements by index; **Merge Sort is the standard for LL.**

---

## Complexity

Time: $O(n \log n)$ → List is split $\log n$ times, and each level of merging takes $O(n)$ work.  
Space: $O(\log n)$ → Due to the recursive call stack (Iterative Merge Sort can achieve $O(1)$ but is significantly more complex).

---

## Similar Problems

- [Merge Two Sorted Lists](https://leetcode.com/problems/merge-two-sorted-lists/) - Easy
- [Insertion Sort List](https://leetcode.com/problems/insertion-sort-list/) - Medium
- [Merge k Sorted Lists](https://leetcode.com/problems/merge-k-sorted-lists/) - Hard
- [Reorder List](https://leetcode.com/problems/reorder-list/) - Medium

---

## Tags and Properties
- #dsa #important #revisit  
- #linkedlist [[Linked List]] #mergesort [[Merge Sort]]
- **Revision Date:** 2026-05-18
- **Problem Link:** [LeetCode - Sort List](https://leetcode.com/problems/sort-list/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-05-20)
- [ ] Day 7 Revision (2026-05-25)
- [ ] Day 15 Revision (2026-06-02)
- [ ] Day 30 Revision (2026-06-17)
