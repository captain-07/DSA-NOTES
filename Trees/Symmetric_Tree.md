---
created: 2026-09-09
revisions:
  - 2026-09-11
  - 2026-09-16
  - 2026-09-24
  - 2026-10-09
---

# Symmetric Tree

---

## Metadata & Placement Tags

- **Folder:** Trees
- **Target Companies:** #Amazon #Google #Microsoft #Facebook #Bloomberg

- **Confidence Checklist:**
  - [ ] Low
  - [ ] Medium
  - [ ] High

- **Concepts:**
  - #binarytree [[Binary Tree]], #dfs [[Depth First Search]], #bfs [[Breadth First Search]], #recursion [[Recursion]]

## Pattern

Tree Comparison (Dual DFS / Two-Pointer Traversal)

---
## Difficulty

Easy #easy

---

## ⚡ Key Idea (Core Insight)

A tree is symmetric if its left and right subtrees are mirror images of each other. Recursively compare two nodes at a time: `left.left` with `right.right` and `left.right` with `right.left`, ensuring their values are equal.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Check mirror condition: `is_mirror(root.left, root.right)` where `node1.val == node2.val` and outer/inner subtrees match.

---

## Approach

### Brute Force
- Perform In-order traversal, collect values into an array, and check if array is a palindrome.
- Fails on structural differences (requires null markers).
- Time: O(N), Space: O(N)

### Optimal
1. Use a recursive helper `_is_mirror(left_node, right_node)`.
2. Base cases: If both are `None`, return `True`. If only one is `None` or values differ, return `False`.
3. Recurse: Compare outer children `(left.left, right.right)` and inner children `(left.right, right.left)`.

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
    def isSymmetric(self, root: TreeNode) -> bool:
        # An empty tree is symmetric
        if not root:
            return True

        # Compare the left and right subtrees
        return self._is_mirror(root.left, root.right)

    def _is_mirror(self, left_node: TreeNode, right_node: TreeNode) -> bool:
        # Both nodes are empty -> symmetric at this branch
        if not left_node and not right_node:
            return True

        # One node is empty, or values don't match -> not symmetric
        if not left_node or not right_node or left_node.val != right_node.val:
            return False

        # Check outer nodes (left.left vs right.right) AND inner nodes (left.right vs right.left)
        outer_match = self._is_mirror(left_node.left, right_node.right)
        inner_match = self._is_mirror(left_node.right, right_node.left)

        return outer_match and inner_match
```

---

## Dry Run (Smart Example)

Input Tree: `[1, 2, 2, null, 3, null, 3]` (Not Symmetric)

| Step | Variables (`left_node`, `right_node`) | Explanation |
| :--- | :--- | :--- |
| 1 | `left_node=2`, `right_node=2` | Values equal (`2 == 2`). Proceed to check subtrees. |
| 2 | `left_node=None`, `right_node=3` (outer) | One is `None`, other is `3`. Base case triggers `False`. |
| 3 | Returns `False` | Short-circuits remaining comparisons. Tree is not symmetric. |

---

## Edge Cases

- **Empty Tree (`root = None`):** Returns `True` by default.
- **Single Node (`root.left = None, root.right = None`):** Returns `True`.
- **Asymmetric Structure:** Left subtree has a left child, but right subtree lacks a right child → Returns `False`.
- **Matching Structure, Different Values:** Structure is identical but values differ → Returns `False`.

---

## Mistakes

- User mistake: No specific note provided.
- Forgetting to handle structural asymmetry where one node is `None` and the other is not.
- Assuming simple In-order traversal array equality guarantees symmetry without handling `None` nodes explicitly.

---

## Complexity

Time: O(N) → Visits every node in the binary tree once.
Space: O(H) → Recursion call stack bounded by tree height $H$ (O(N) worst-case for skewed tree, O(log N) for balanced).

---

## Similar Problems

- [Same Tree](https://leetcode.com/problems/same-tree/) - Easy
- [Invert Binary Tree](https://leetcode.com/problems/invert-binary-tree/) - Easy
- [Subtree of Another Tree](https://leetcode.com/problems/subtree-of-another-tree/) - Easy

---

## Tags and Properties

- #dsa #important #revisit
- #binarytree #dfs #recursion
- [[Binary Tree]] [[Depth First Search]] [[Recursion]]
- **Last Revised:** 2026-09-09
- **Problem Link:** [Symmetric Tree - LeetCode](https://leetcode.com/problems/symmetric-tree/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-09-11)
- [ ] Day 7 Revision (2026-09-16)
- [ ] Day 15 Revision (2026-09-24)
- [ ] Day 30 Revision (2026-10-09)
