---
created: 2026-09-02
revisions:
  - 2026-09-04
  - 2026-09-09
  - 2026-09-17
  - 2026-10-02
---

# Traversal Of Binary Tree Iterative

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Google #Microsoft #Facebook #Apple

- **Confidence Checklist:**
  - [ ] Low
  - [ ] Medium
  - [ ] High

- **Concepts:**
  - #binarytree [[Binary Tree]], #stack [[Stack]], #dfs [[Depth First Search]]

---
## Pattern

Stack-based DFS Simulation

---
## Difficulty

Medium #medium

---

## ⚡ Key Idea (Core Insight)

Use an explicit stack to simulate the call stack of recursion.
- **Preorder (N-L-R):** Push Right child first, then Left child, so Left is processed first.
- **Inorder (L-N-R):** Push all Left nodes to stack until null; pop, visit, then move to Right child.
- **Postorder (L-R-N):** Push Root to Stack 1, pop and push to Stack 2, then push Left and Right to Stack 1. Stack 2 yields Postorder when popped.

---

## ⚡ Quick Recall (VERY IMPORTANT)

- **Preorder:** Stack processing: Node -> Push Right -> Push Left.
- **Inorder:** Go deep Left -> Pop & Process -> Go Right.
- **Postorder:** Modified Preorder (Root-Right-Left) reversed using a 2nd stack (Left-Right-Root).

---

## Approach

### Brute Force
- Use recursion for traversal (implicit call stack).
- **Time:** O(N), **Space:** O(N) auxiliary recursion stack space.

### Optimal
- Use explicit `List` and `Stack` data structures to traverse iteratively without system stack overflow.

---

## Code (Python)

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right

class Solution:
    def preorderTraversal(self, root: TreeNode) -> list[int]:
        if not root:
            return []
        res, stack = [], [root]
        while stack:
            node = stack.pop()
            res.append(node.val)
            if node.right:
                stack.append(node.right)
            if node.left:
                stack.append(node.left)
        return res

    def inorderTraversal(self, root: TreeNode) -> list[int]:
        res, stack = [], []
        curr = root
        while curr or stack:
            while curr:
                stack.append(curr)
                curr = curr.left
            curr = stack.pop()
            res.append(curr.val)
            curr = curr.right
        return res

    def postorderTraversal(self, root: TreeNode) -> list[int]:
        if not root:
            return []
        res, s1 = [], [root]
        s2 = []
        while s1:
            node = s1.pop()
            s2.append(node)
            if node.left:
                s1.append(node.left)
            if node.right:
                s1.append(node.right)
        while s2:
            res.append(s2.pop().val)
        return res
```

---

## Dry Run (Smart Example)

Tree: `[1, 2, 3]` (1 is root, 2 is left child, 3 is right child)

| Step | Stack / Pointer State | Explanation |
| :--- | :--- | :--- |
| 1 (Preorder) | `stack=[1]` | Pop `1`, `res=[1]`. Push `3` (right), then `2` (left). `stack=[3, 2]` |
| 2 (Preorder) | `stack=[3, 2]` | Pop `2`, `res=[1, 2]`. No children. Next pop `3`, `res=[1, 2, 3]`. |
| 3 (Inorder) | `curr=1`, `stack=[]` | Push `1`, move to `2`. Push `2`, move `curr=None`. |
| 4 (Inorder) | `stack=[1, 2]` | Pop `2`, `res=[2]`. Pop `1`, `res=[2, 1]`, `curr=3`. Push & pop `3` -> `[2, 1, 3]`. |
| 5 (Postorder)| `s1=[1]`, `s2=[]` | Pop `1` to `s2`. Push `2` (left) & `3` (right) to `s1`. `s1=[2, 3]`, `s2=[1]`. |
| 6 (Postorder)| Pop `s1` to `s2` | `s2` becomes `[1, 3, 2]`. Popping `s2` yields `[2, 3, 1]`. |

---

## Edge Cases

- **Empty Tree (`root = None`):** Return empty array `[]`.
- **Single Node:** Stack initialized and processed in 1 iteration.
- **Skewed Tree (Left/Right only):** Stack length equals tree height N.

---

## Mistakes

- **User Mistake:** Mixing up iterative approaches across Preorder, Inorder, and Postorder traversals.
- Forgetting to push **Right child first** in Preorder stack (causes Left child to process second).
- Null pointer access on `curr.left` or `curr.right` without checked conditionals.
- Trying to implement Postorder with a single stack without tracking the `last_visited` node.

---

## Complexity

Time: O(N) → Every node is pushed and popped from the stack at most twice.
Space: O(N) → Stack space proportional to tree height/nodes.

---

## Similar Problems

- [Binary Tree Preorder Traversal](https://leetcode.com/problems/binary-tree-preorder-traversal/) - Easy
- [Binary Tree Inorder Traversal](https://leetcode.com/problems/binary-tree-inorder-traversal/) - Easy
- [Binary Tree Postorder Traversal](https://leetcode.com/problems/binary-tree-postorder-traversal/) - Easy
- [Binary Tree Level Order Traversal](https://leetcode.com/problems/binary-tree-level-order-traversal/) - Medium

---

## Tags and Properties

- #dsa #important #revisit #binarytree #iterativetraversal
- [[Binary Tree]], [[Stack]], [[Depth First Search]]
- **Revision Date:** 2026-09-02
- **Problem Link:** [Binary Tree Inorder Traversal](https://leetcode.com/problems/binary-tree-inorder-traversal/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-09-04)
- [ ] Day 7 Revision (2026-09-09)
- [ ] Day 15 Revision (2026-09-17)
- [ ] Day 30 Revision (2026-10-02)
