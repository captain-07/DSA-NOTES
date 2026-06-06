---
created: 2026-06-06
revisions:
  - 2026-06-08
  - 2026-06-13
  - 2026-06-21
  - 2026-07-06
---

# Reverse A Stack

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Microsoft #Adobe #GoldmanSachs #Walmart

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #recursion [[Recursion]]
  - #stack [[Stack]]

## Pattern

Recursive Backtracking + Bottom Insertion  

---
## Difficulty

Medium  
#medium

---

## ⚡ Key Idea (Core Insight)

The problem constraints typically forbid using additional data structures (like a queue or another stack). The core insight is using the **Function Call Stack** as the implicit storage. You pop the top element, recursively reverse the remaining stack, and then use a helper function to insert the popped element at the very **bottom** of the now-reversed stack.

---

## ⚡ Quick Recall (VERY IMPORTANT)

"Pop top, reverse the rest, insert popped at bottom."  
(Requires two recursive functions: one to reverse, one to insert at bottom).

---

## Approach

### Brute Force
- Pop all elements into an auxiliary Queue or another Stack and then push them back.
- Time: O(N) | Space: O(N) (Extra Data Structure)

### Optimal (Recursive)
1. **Reverse Function:** 
   - Base case: If stack is empty, return.
   - Recursive step: Pop `top`, call `reverse`, then `insertAtBottom(top)`.
2. **InsertAtBottom Function:**
   - Base case: If stack is empty, push the element and return.
   - Recursive step: Pop `top`, call `insertAtBottom(element)`, then push `top` back.
- Time: O(N²) | Space: O(N) (Recursion Depth)

---

## Code (Python)

```python
class Solution:
    def reverseStack(self, stack: list[int]) -> None:
        """
        Reverses the stack in-place using recursion.
        """
        if not stack:
            return
        
        # Step 1: Pop the top element
        top_element = stack.pop()
        
        # Step 2: Recursively reverse the remaining stack
        self.reverseStack(stack)
        
        # Step 3: Insert the popped element at the bottom
        self.insertAtBottom(stack, top_element)

    def insertAtBottom(self, stack: list[int], element: int) -> None:
        """
        Helper function to insert an element at the bottom of the stack.
        """
        if not stack:
            stack.append(element)
            return
        
        # Pop current top to reach the bottom
        top = stack.pop()
        self.insertAtBottom(stack, element)
        
        # Push the top back after insertion at bottom
        stack.append(top)
```

---

## Dry Run (Smart Example)

Input: `stack = [3, 2, 1]` (Top is 1)

| Step | Function | Stack State | Action |
| :--- | :--- | :--- | :--- |
| 1 | `reverseStack` | `[3, 2]` | Pop `1`, Call `reverseStack` |
| 2 | `reverseStack` | `[3]` | Pop `2`, Call `reverseStack` |
| 3 | `reverseStack` | `[]` | Pop `3`, Call `reverseStack` |
| 4 | Base Case | `[]` | Return to Step 3 |
| 5 | `insertAtBottom` | `[3]` | Insert `3` at bottom of `[]` |
| 6 | `insertAtBottom` | `[2, 3]` | Insert `2` at bottom of `[3]` |
| 7 | `insertAtBottom` | `[1, 2, 3]` | Insert `1` at bottom of `[2, 3]` |

---

## Edge Cases

- **Empty Stack:** Should return immediately without error.
- **Single Element:** Stack remains unchanged.
- **Duplicates:** The recursive logic naturally handles duplicate values correctly.
- **Negative Numbers:** Handled naturally by the stack's integer storage.

---

## Mistakes

- Using an auxiliary data structure when the interviewer expects O(1) **extra** space (recursion stack excluded).
- Forgetting that `insertAtBottom` also needs to be recursive or use a loop.
- **User mistake:** No specific note provided.

---

## Complexity

Time: O(N²) → For each of the N elements in `reverseStack`, we call `insertAtBottom` which takes O(N) time.  
Space: O(N) → Maximum depth of the recursion stack is N.

---

## Similar Problems

- [Reverse a String using Stack](https://www.geeksforgeeks.org/stack-set-3-reverse-string-using-stack/) - Easy
- [Sort a Stack](https://www.geeksforgeeks.org/sort-a-stack-using-recursion/) - Medium
- [Delete Middle Element of a Stack](https://www.geeksforgeeks.org/delete-middle-element-stack/) - Easy
- [Reverse Linked List](https://leetcode.com/problems/reverse-linked-list/) - Easy

---

## Tags and Properties
  - #dsa #important #revisit #recursion #stacks
  - [[Recursion]] [[Stack]]
  - **Revision Date:** 2026-06-06
  - **Problem Link:** [Reverse a Stack using Recursion - GFG](https://www.geeksforgeeks.org/problems/reverse-a-stack/1)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-06-08)
- [ ] Day 7 Revision (2026-06-13)
- [ ] Day 15 Revision (2026-06-21)
- [ ] Day 30 Revision (2026-07-06)
