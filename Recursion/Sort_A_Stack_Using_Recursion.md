---
created: 2026-06-06
revisions:
  - 2026-06-08
  - 2026-06-13
  - 2026-06-21
  - 2026-07-06
---

# Sort A Stack Using Recursion

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Microsoft #GoldmanSachs #Adobe #Walmart

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #recursion [[Recursion]]
  - #stack [[Stack]]
  - #backtracking [[Backtracking]]

## Pattern

Recursion (Decomposition + Sorted Insertion)

---
## Difficulty

Medium  
#medium

---

## ⚡ Key Idea (Core Insight)

The problem relies on two recursive phases:
1. **Unwinding:** Pop all elements until the stack is empty, storing them in the function call stack.
2. **Re-insertion:** As recursion unfolds, use a helper function to insert each element back into the stack at its correct sorted position.

---

## ⚡ Quick Recall (VERY IMPORTANT)

"Pop everything out recursively to empty the stack, then `sortedInsert` each element back into the stack."

---

## Approach

### Brute Force
- Convert the stack to an array, sort the array using a standard sorting algorithm, and push elements back.
- Time: $O(N \log N)$ | Space: $O(N)$

### Better
- Use an auxiliary stack. Pop from the main stack and push into the auxiliary stack in a sorted manner iteratively.
- Time: $O(N^2)$ | Space: $O(N)$

### Optimal
- **In-place Recursion:**
  - `sortStack(s)`: Base case: empty. Recursive call: `temp = s.pop()`, `sortStack(s)`, `sortedInsert(s, temp)`.
  - `sortedInsert(s, val)`: Base case: empty or `val > s.peek()`. Recursive step: `temp = s.pop()`, `sortedInsert(s, val)`, `s.push(temp)`.
- Time: $O(N^2)$ | Space: $O(N)$ (Recursive call stack)

---

## Code (Python)

```python
class Solution:
    def sort_stack(self, stack):
        """
        Sorts the stack in-place using recursion.
        Standard convention: Smallest at bottom, Largest at top.
        """
        # Base Case: If stack is empty, it's already sorted
        if not stack:
            return
        
        # Step 1: Pop the top element
        temp = stack.pop()
        
        # Step 2: Sort the remaining stack
        self.sort_stack(stack)
        
        # Step 3: Insert the popped element back in sorted order
        self.sorted_insert(stack, temp)

    def sorted_insert(self, stack, element):
        """
        Helper to insert element into a sorted stack.
        """
        # Base Case: Stack is empty or current element is greater than top
        if not stack or element > stack[-1]:
            stack.append(element)
            return
        
        # If element is smaller, pop top and recurse
        temp = stack.pop()
        self.sorted_insert(stack, element)
        
        # Push the held element back after insertion
        stack.append(temp)
```

---

## Dry Run (Smart Example)

**Input:** `stack = [5, -2, 9, 1]` (Top is 1)

| Step | Operation | Call Stack State (Recursive) | Stack State (Physical) |
| :--- | :--- | :--- | :--- |
| 1 | `sort_stack` | Pop [1, 9, -2, 5] in order | `[]` (Empty) |
| 2 | `sorted_insert(5)` | Base case: empty | `[5]` |
| 3 | `sorted_insert(-2)` | -2 < 5: Pop 5, Insert -2, Push 5 | `[-2, 5]` |
| 4 | `sorted_insert(9)` | 9 > 5: Push 9 | `[-2, 5, 9]` |
| 5 | `sorted_insert(1)` | 1 < 9, 1 < 5: Pop 9, Pop 5, Insert 1, Push 5, Push 9 | `[-2, 1, 5, 9]` |

---

## Edge Cases

- **Empty Stack:** Should return immediately without error.
- **Single Element:** Base case handled; no sorting needed.
- **All Identical Elements:** `sorted_insert` will always hit the `element > stack[-1]` (or `>=`) condition and push immediately.
- **Reverse Sorted Stack:** Maximum recursive calls in `sorted_insert` for every element.

---

## Mistakes

- **Base Case Omission:** Forgetting to check `if not stack` in `sorted_insert` leads to `IndexError`.
- **Comparison Logic:** Flipping `>` to `<` results in a descending sort instead of ascending.
- **Missing User Note:** User mistake: No specific note provided.

---

## Complexity

Time: $O(N^2)$ → Each element $N$ is inserted using `sorted_insert`, which itself takes $O(N)$ in the worst case.  
Space: $O(N)$ → Maximum depth of the recursion tree is $N$ for both functions.

---

## Similar Problems

- [Reverse a Stack using Recursion](https://www.geeksforgeeks.org/reverse-a-stack-using-recursion/) - Medium
- [Delete Middle Element of a Stack](https://www.geeksforgeeks.org/delete-middle-element-stack/) - Easy
- [Insert at Bottom of Stack](https://www.geeksforgeeks.org/program-to-insert-an-element-at-the-bottom-of-a-stack/) - Easy
- [Sort a Stack (Iterative)](https://leetcode.com/problems/sort-an-array/) - Medium (Conceptually related)

---

## Tags and Properties
  - #dsa #important #revisit #recursion #stack
  - [[Recursion]] [[Stack]]
  - Revision Date: 2026-06-06
  - **Problem Link:** [Sort a Stack - GeeksforGeeks](https://www.geeksforgeeks.org/problems/sort-a-stack/1)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-06-08)
- [ ] Day 7 Revision (2026-06-13)
- [ ] Day 15 Revision (2026-06-21)
- [ ] Day 30 Revision (2026-07-06)
