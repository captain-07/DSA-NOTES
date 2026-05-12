---
created: 2026-05-12
revisions:
  - 2026-05-14
  - 2026-05-19
  - 2026-05-27
  - 2026-06-11
---

# Length Of Loop In Ll

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Microsoft #Samsung #Adobe #Walmart

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #linkedlist [[Linked List]]
  - #twopointers [[Two Pointers]]
  - #floydscycle [[Floyd's Cycle Finding Algorithm]]

---
## Pattern

Two Pointers (Fast & Slow)  

---
## Difficulty

Medium  
#medium

---
## ⚡ Key Idea (Core Insight)

Use **Floyd’s Cycle-Finding Algorithm** to detect the loop. Once `slow` and `fast` pointers meet, the list is guaranteed to have a loop. To find the length, keep one pointer fixed and move the other until it hits the fixed pointer again, incrementing a counter.

---
## ⚡ Quick Recall (VERY IMPORTANT)

Detect loop with `slow`/`fast`. When they meet, initialize `count = 1`, move `slow = slow.next` until it reaches `fast` again.

---
## Approach

### Brute Force
- Use a **HashMap** or **HashSet** to store nodes. Traverse the list; the first node seen twice identifies the loop start. Store the "timestamp" or index to calculate `current_index - stored_index`.
- **Time:** O(N)
- **Space:** O(N)

### Optimal
1. Initialize `slow` and `fast` at `head`.
2. Move `slow` by 1 and `fast` by 2.
3. If they meet, a loop exists.
4. **Counting Logic:** Keep `fast` at the meeting point. Move `slow = slow.next` and initialize `cnt = 1`.
5. Continue `slow = slow.next` and `cnt += 1` until `slow == fast`.
6. Return `cnt`.
- **Time:** O(N)
- **Space:** O(1)

---
## Code (Python)

```python
class Solution:
    def countNodesInLoop(self, head):
        slow = head
        fast = head
        
        # Step 1: Detect Loop
        while fast and fast.next:
            slow = slow.next
            fast = fast.next.next
            
            # Step 2: Loop found
            if slow == fast:
                return self.count_length(slow)
        
        return 0 # No loop
        
    def count_length(self, loop_node):
        # User Mistake Fix: Start count at 1, move temp first
        cnt = 1
        temp = loop_node.next
        
        while temp != loop_node:
            cnt += 1
            temp = temp.next
        return cnt
```

---
## Dry Run (Smart Example)

**Input:** `1 -> 2 -> 3 -> 4 -> 5 -> (back to 3)`

| Step | slow | fast | Explanation |
| :--- | :--- | :--- | :--- |
| 1 | 2 | 3 | Initial movement. |
| 2 | 3 | 5 | fast moves twice as fast. |
| 3 | 4 | 4 | **Meeting Point!** slow and fast meet at node 4. |
| 4 | temp=5 | loop=4 | Start count: `cnt=1`. `temp` moves to 5. |
| 5 | temp=3 | loop=4 | `temp` moves to 3. `cnt=2`. |
| 6 | temp=4 | loop=4 | `temp` hits `loop_node`. `cnt=3`. Return. |

---
## Edge Cases

- **No Loop:** `fast` reaches `None`. Return 0.
- **Single Node Loop:** `1 -> 1`. `slow` and `fast` meet at 1. Count is 1.
- **Whole List is Loop:** `1 -> 2 -> 1`.
- **Very Large Loop:** `cnt` logic remains O(N).

---
## Mistakes

- **The inside logic of cnt:** Starting `cnt` at 0 and checking `temp != slow` immediately (the loop will never run if `temp` starts at `slow`).
- **Pointer Null Checks:** Forgetting to check `while fast and fast.next`.
- **Wrong Return:** Returning `slow` or `fast` instead of the integer `cnt`.

---
## Complexity

Time: O(N) → Linear traversal to find meet point + max one loop cycle to count.  
Space: O(1) → Only constant extra pointers used.

---
## Similar Problems

- [Linked List Cycle](https://leetcode.com/problems/linked-list-cycle/) - Easy
- [Linked List Cycle II](https://leetcode.com/problems/linked-list-cycle-ii/) - Medium
- [Find the Duplicate Number](https://leetcode.com/problems/find-the-duplicate-number/) - Medium

---
## Tags and Properties
- #dsa #important #revisit #linkedlist #floyd
- [[Linked List]] [[Two Pointers]]
- **Problem Link:** [GeeksforGeeks - Find Length of Loop](https://www.geeksforgeeks.org/problems/find-length-of-loop/1)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-05-14)
- [ ] Day 7 Revision (2026-05-19)
- [ ] Day 15 Revision (2026-05-27)
- [ ] Day 30 Revision (2026-06-11)
