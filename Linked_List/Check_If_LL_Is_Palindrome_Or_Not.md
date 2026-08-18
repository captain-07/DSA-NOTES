---
created: 2026-05-15
revisions:
  - 2026-05-17
  - 2026-05-22
  - 2026-05-30
  - 2026-06-14
---

# Check If LL Is Palindrome Or Not

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Microsoft #Google #LinkedIn #Adobe #Bloomberg

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #linkedlist [[Linked List]]
  - #twopointers [[Two Pointers]]
  - #recursion [[Recursion]]

---
## Pattern

Slow & Fast Pointers + In-place Reversal

---
## Difficulty

Easy / #easy

---

## ⚡ Key Idea (Core Insight)

Use the **Slow and Fast pointer** technique to identify the midpoint of the list. Reverse the **second half** of the linked list in-place and compare its values against the first half starting from the head.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Find middle (Slow/Fast) → Reverse 2nd half → Compare with 1st half → Result.

---

## Approach

### Brute Force
- Copy all node values into a Python list and use the two-pointer approach to check if the list is a palindrome.
- **Time:** O(N) | **Space:** O(N)

### Better (Recursive)
- Use a global pointer at the head and recurse to the tail. Compare values on the way back up the call stack.
- **Time:** O(N) | **Space:** O(N) (Recursion Stack)

### Optimal
1. **Find Middle:** Use `slow` and `fast` pointers (fast moves twice as fast).
2. **Reverse:** Reverse the second half of the list starting from `slow.next`.
3. **Compare:** Traverse both halves simultaneously; if any values differ, it is not a palindrome.
4. **Restore (Optional):** Re-reverse the second half to maintain original list structure.
- **Time:** O(N) | **Space:** O(1)

---

## Code (Python)

```python
class Solution:
    def isPalindrome(self, head: Optional[ListNode]) -> bool:
        if not head or not head.next:
            return True
            
        # 1. Find the end of the first half
        slow = fast = head
        while fast.next and fast.next.next:
            slow = slow.next
            fast = fast.next.next
            
        # 2. Reverse the second half
        second_half_head = self.reverse_list(slow.next)
        
        # 3. Check for palindrome
        first_ptr = head
        second_ptr = second_half_head
        result = True
        while second_ptr:
            if first_ptr.val != second_ptr.val:
                result = False
                break
            first_ptr = first_ptr.next
            second_ptr = second_ptr.next
            
        # 4. Optional: Restore the list structure
        # slow.next = self.reverse_list(second_half_head)
        
        return result

    def reverse_list(self, head):
        prev = None
        curr = head
        while curr:
            next_node = curr.next
            curr.next = prev
            prev = curr
            curr = next_node
        return prev
```

---

## Dry Run (Smart Example)

**Input:** `1 -> 2 -> 3 -> 2 -> 1`

| Step | Variables | Explanation |
| :--- | :--- | :--- |
| **Initial** | `slow=1`, `fast=1` | Start pointers at head. |
| **Find Mid** | `slow=3`, `fast=1 (tail)` | `fast` reaches end; `slow` is at the middle. |
| **Reverse** | `rev_head=1 -> 2` | Reverses the part after `slow` (`2 -> 1`). |
| **Compare** | `1==1`, `2==2` | Compare `head (1,2)` with `rev_head (1,2)`. |
| **End** | `True` | All compared nodes matched. |

---

## Edge Cases

- **Single Node:** Always returns `True`.
- **Two Nodes:** `[1, 2]` returns `False`, `[1, 1]` returns `True`.
- **Even Length:** `[1, 2, 2, 1]` requires precise middle handling (`slow` must end at first `2`).
- **Duplicates:** `[1, 1, 1]` handled naturally by comparison.

---

## Mistakes

- **Reversing the second half incorrectly:** Forgetting to handle the `None` termination or losing the head of the reversed segment.
- **Off-by-one in Midpoint:** Choosing the wrong node as the start of the second half in even-length lists.
- **Not restoring the list:** In real interviews, mutating the input without restoring it is often frowned upon.
- **Null Checks:** Failing to check `head.next` before finding middle.

---

## Complexity

- **Time:** O(N) → One pass to find middle, one pass to reverse half, one pass to compare.
- **Space:** O(1) → In-place reversal uses no extra data structures.

---

## Similar Problems

- [Palindrome Linked List](https://leetcode.com/problems/palindrome-linked-list/) - Easy
- [Reverse Linked List](https://leetcode.com/problems/reverse-linked-list/) - Easy
- [Middle of the Linked List](https://leetcode.com/problems/middle-of-the-linked-list/) - Easy
- [Reorder List](https://leetcode.com/problems/reorder-list/) - Medium

---

## Tags and Properties
  - #dsa #important #revisit  
  - #linkedlist #twopointers #inplace  
  - [[Linked List]] [[Two Pointers]]
  - **Revision Date:** 2026-05-15
  - **Problem Link:** [LeetCode - Palindrome Linked List](https://leetcode.com/problems/palindrome-linked-list/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-05-17)
- [ ] Day 7 Revision (2026-05-22)
- [ ] Day 15 Revision (2026-05-30)
- [ ] Day 30 Revision (2026-06-14)
