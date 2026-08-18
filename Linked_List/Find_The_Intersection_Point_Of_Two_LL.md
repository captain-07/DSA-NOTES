---
created: 2026-05-27
revisions:
  - 2026-05-29
  - 2026-06-03
  - 2026-06-11
  - 2026-06-26
---

# Find The Intersection Point Of Two LL

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Microsoft #Adobe #LinkedIn #GoldmanSachs #Google

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #linkedlist [[Linked List]]
  - #twopointers [[Two Pointers]]
  - #hashmap [[HashMap]]

---
## Pattern

Two Pointers (Length Alignment / Head Switching)  
Hashing (Node Tracking)

---
## Difficulty

Medium  
#medium

---

## ⚡ Key Idea (Core Insight)

The difference in lengths is the only obstacle. By switching the pointer to the head of the *opposite* list after reaching the end, both pointers traverse exactly `LengthA + LengthB` distance, neutralizing the length difference and forcing them to meet at the intersection point.

---

## ⚡ Quick Recall (VERY IMPORTANT)

`p1 = headA`, `p2 = headB`. While `p1 != p2`: `p1 = p1.next if p1 else headB`, `p2 = p2.next if p2 else headA`.

---

## Approach

### Brute Force
- Nested loops: For each node in List A, traverse List B to check if the same node exists.
- **Time:** O(N × M) | **Space:** O(1)

### Better
- Store all node references of List A in a Set/HashMap. Traverse List B and check if current node exists in the Set.
- **Time:** O(N + M) | **Space:** O(N) or O(M)

### Optimal
1. Initialize two pointers `currA` and `currB` at the heads.
2. Traverse both; when a pointer reaches `None`, redirect it to the head of the **other** list.
3. If they intersect, they will meet at the intersection node.
4. If they don't intersect, they will both reach `None` at the same time (after switching).
- **Time:** O(N + M) | **Space:** O(1)

---

## Code (Python)

```python
class Solution:
    def getIntersectionNode(self, headA: ListNode, headB: ListNode) -> Optional[ListNode]:
        if not headA or not headB:
            return None
        
        ptrA, ptrB = headA, headB
        
        # In the second iteration, pointers are aligned by length difference
        while ptrA != ptrB:
            # Switch to other head if end is reached
            ptrA = ptrA.next if ptrA else headB
            ptrB = ptrB.next if ptrB else headA
            
        return ptrA # Either intersection node or None
```

---

## Dry Run (Smart Example)

**Input:** 
A: [4, 1, 8, 4, 5]
B: [5, 6, 1, 8, 4, 5]
Intersection: Node(8)

| Step | ptrA (Value) | ptrB (Value) | Explanation |
| :--- | :--- | :--- | :--- |
| 1 | 4 | 5 | Start at heads. |
| 2 | 1 | 6 | Moving normally. |
| 3 | 8 | 1 | Moving normally. |
| 4 | 4 | 8 | Moving normally. |
| 5 | 5 | 4 | ptrA is near end. |
| 6 | None | 5 | ptrA hits None. |
| 7 | **5 (headB)** | None | ptrA switches to B, ptrB hits None. |
| 8 | 6 | **4 (headA)** | ptrB switches to A. |
| 9 | 1 | 1 | Pointers are now synced in distance. |
| 10 | **8** | **8** | **Intersection Found!** |

---

## Edge Cases

- **No Intersection:** Both pointers will eventually hit `None` simultaneously and loop will exit.
- **Lists of Same Length:** Pointers meet in the first pass if they intersect.
- **One List is Empty:** Handled by initial `None` check.
- **Intersect at Head:** `ptrA == ptrB` immediately.

---

## Mistakes

- Using `.val` instead of comparing the **node object/reference**.
- Forgetting to handle the `None` case, leading to infinite loops if no intersection exists.
- **User mistake:** No specific note provided. (Ensure you understand the "Switching Heads" intuition before the interview).

---

## Complexity

Time: O(N + M) → Each node is visited at most twice.  
Space: O(1) → Only two pointer variables used.

---

## Similar Problems

- [Linked List Cycle](https://leetcode.com/problems/linked-list-cycle/) - Easy
- [Middle of the Linked List](https://leetcode.com/problems/middle-of-the-linked-list/) - Easy
- [Remove Nth Node From End of List](https://leetcode.com/problems/remove-nth-node-from-end-of-list/) - Medium

---

## Tags and Properties
- #dsa #important #revisit  
- #linkedlist [[Linked List]] #twopointers [[Two Pointers]]
- **Revision Date:** 2026-05-27
- **Problem Link:** [LeetCode - Intersection of Two Linked Lists](https://leetcode.com/problems/intersection-of-two-linked-lists/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-05-29)
- [ ] Day 7 Revision (2026-06-03)
- [ ] Day 15 Revision (2026-06-11)
- [ ] Day 30 Revision (2026-06-26)
