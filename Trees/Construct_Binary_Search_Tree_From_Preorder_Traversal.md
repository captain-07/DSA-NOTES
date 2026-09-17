---
created: 2026-09-17
revisions:
  - 2026-09-19
  - 2026-09-24
  - 2026-10-02
  - 2026-10-17
---

# Construct Binary Search Tree From Preorder Traversal

---

## Metadata & Placement Tags

- **Folder:** Trees
- **Target Companies:** #Amazon #Google #Microsoft #LeetCode
- **Confidence Checklist:**
  - [ ] Low
  - [ ] Medium
  - [ ] High

- **Concepts:**
  - #tree [[Trees]], #bst [[Binary Search Tree]], #recursion [[Recursion]], #stack [[Monotonic Stack]]

## Pattern

Monotonic Stack / Recursion with Upper Bound

---
## Difficulty

Medium #medium

---

## ⚡ Key Idea (Core Insight)

Maintain a upper limit (`bound`) for the current subtree. A node can only be placed in the current BST position if its value is less than `bound`. Otherwise, return `None` so it bubbles up to the right parent.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Pass `bound` down recursively. Left child bound is `curr_val`, right child bound is parent's `bound`. Use an instance pointer/index to track array position.

---

## Approach

### Brute Force
- Insert elements one by one into BST starting from root.
- Time: O(N^2) worst case (skewed tree), Space: O(N) recursion stack.

### Better
- Sort preorder to get inorder traversal, then construct tree using preorder and inorder.
- Time: O(N log N) sorting + O(N) tree construction, Space: O(N) for inorder array & recursion stack.

### Optimal 1: Recursion with Bound
- Track current index with a class attribute (`self.index`). Build left subtree with upper bound `curr_node.val` and right subtree with current upper bound `bound`.
- Time: O(N), Space: O(H) call stack where H is tree height.

### Optimal 2: Iterative using Monotonic Stack
- Push nodes to stack while moving left. When encountering a larger value, pop nodes from stack until finding the proper parent for the right child.
- Time: O(N), Space: O(H) stack depth.

---

## Code (Python)

### Optimal 1: Recursion with Bound (Class Index)

```python
class Solution:
    def bstFromPreorder(self, preorder: list[int]) -> Optional[TreeNode]:
        # Pointer to track current element in preorder traversal
        self.index = 0
        return self.build_bst(preorder, float('inf'))

    def build_bst(self, preorder: list[int], bound: float) -> Optional[TreeNode]:
        # Base case: all elements used or current element exceeds upper bound
        if self.index >= len(preorder) or preorder[self.index] > bound:
            return None

        # Create root node with current element and advance pointer
        root_val = preorder[self.index]
        self.index += 1
        root = TreeNode(root_val)

        # Left subtree values must be less than current node's value
        root.left = self.build_bst(preorder, root_val)
        # Right subtree values must be less than parent bound
        root.right = self.build_bst(preorder, bound)

        return root
```

### Optimal 2: Iterative Monotonic Stack

```python
class Solution:
    def bstFromPreorder(self, preorder: list[int]) -> Optional[TreeNode]:
        if not preorder:
            return None

        root = TreeNode(preorder[0])
        stack = [root]

        for value in preorder[1:]:
            node = TreeNode(value)

            # If value is less than top of stack, it goes to left child
            if value < stack[-1].val:
                stack[-1].left = node
            else:
                # Pop elements to find the last node smaller than current value
                parent = stack[-1]
                while stack and stack[-1].val < value:
                    parent = stack.pop()
                parent.right = node

            stack.append(node)

        return root
```

---

## Dry Run (Smart Example)

Input: `preorder = [8, 5, 1, 7, 10, 12]`

| Step | Call / Variables | Explanation |
| :--- | :--- | :--- |
| 1 | `build_bst(preorder, inf)` | `index=0`, val=8 <= inf. Root = 8. `index` becomes 1. Recurse left with `bound=8`. |
| 2 | `build_bst(preorder, 8)` | `index=1`, val=5 <= 8. Node 8.left = 5. `index` becomes 2. Recurse left with `bound=5`. |
| 3 | `build_bst(preorder, 5)` | `index=2`, val=1 <= 5. Node 5.left = 1. `index` becomes 3. Recurse left with `bound=1`. |
| 4 | `build_bst(preorder, 1)` | `index=3`, val=7 > 1. Returns `None`. Backtrack to 1.right with `bound=5`. |
| 5 | `build_bst(preorder, 5)` | `index=3`, val=7 > 5. Returns `None`. Backtrack to 5.right with `bound=8`. |
| 6 | `build_bst(preorder, 8)` | `index=3`, val=7 <= 8. Node 5.right = 7. `index` becomes 4. |

---

## Edge Cases

- **Single Element `[1]`:** Base case returns single root without recursive stack overflow.
- **Strictly Decreasing `[5, 4, 3, 2, 1]`:** Skewed left tree; upper bound updates every step correctly.
- **Strictly Increasing `[1, 2, 3, 4, 5]`:** Skewed right tree; continuously bubbles up to root.

---

## Mistakes

- **User Mistake: `use self.i`** — Primitive integer types (`int`) are immutable in Python. Passing `index` as an integer variable `helper(preorder, i, bound)` does not persist state mutations across recursive frames. You MUST use an instance variable `self.index`, an array/list wrapper `[0]`, or an iterator.
- Passing single boundary values without taking lower/upper properties into account.

---

## Complexity

Time: O(N) → Each element in `preorder` is processed exactly once.
Space: O(H) → Call stack / explicit stack depth is proportional to tree height (O(N) worst case, O(log N) best case).

---

## Similar Problems

- [Construct Binary Tree from Preorder and Inorder Traversal](https://leetcode.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/) - Medium
- [Serialize and Deserialize BST](https://leetcode.com/problems/serialize-and-deserialize-bst/) - Medium
- [Verify Preorder Sequence in Binary Search Tree](https://leetcode.com/problems/verify-preorder-sequence-in-binary-search-tree/) - Medium

---

## Tags and Properties

- #dsa #important #revisit #trees #bst #recursion #stack
- [[Trees]], [[Binary Search Tree]], [[Monotonic Stack]], [[Recursion]]
- **Problem Link:** [LeetCode - Construct Binary Search Tree from Preorder Traversal](https://leetcode.com/problems/construct-binary-search-tree-from-preorder-traversal/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-09-19)
- [ ] Day 7 Revision (2026-09-24)
- [ ] Day 15 Revision (2026-10-02)
- [ ] Day 30 Revision (2026-10-17)
