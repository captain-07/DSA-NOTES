---
created: 2026-09-06
revisions:
  - 2026-09-08
  - 2026-09-13
  - 2026-09-21
  - 2026-10-06
---

# Boundary Traversal of Binary Tree

---

## Metadata & Placement Tags

- **Folder:** Trees
- **Target Companies:** #Amazon #Microsoft #Google #Paytm #Flipkart

- **Confidence Checklist:**
  - [ ] Low
  - [ ] Medium
  - [ ] High

- **Concepts:**
  - #tree [[Trees]], #dfs [[DFS]], #bfs [[BFS]], #recursion [[Recursion]]

## Pattern

Tree Traversal (Boundary Decomposition: Left Boundary + Leaf Nodes + Right Boundary)

---
## Difficulty

Medium
#medium

---

## ⚡ Key Idea (Core Insight)

- Divide boundary traversal into three distinct sub-problems: **Left boundary** (top-down), **Leaf nodes** (left-to-right via DFS), and **Right boundary** (bottom-up using reverse order).
- **Critical Control Flow:** To maintain outer perimeter continuity, if a left child is missing while scanning the left boundary, fallback to the right child (`if not node.left: node = node.right`). Vice versa for the right boundary (`if not node.right: node = node.left`).

---

## ⚡ Quick Recall (VERY IMPORTANT)

- Traversal = Root (if not leaf) + Left Boundary (excluding leaves) + All Leaves (DFS) + Reverse Right Boundary (excluding leaves).
- Always exclude leaf nodes during left/right boundary scanning to avoid duplicate additions!

---

## Approach

### Brute Force
- Store all nodes in a standard DFS/BFS traversal, then visually map and filter perimeter nodes manually.
- Time Complexity: $O(N)$, Space Complexity: $O(N)$

### Optimal
- **Step 1:** Add root value to result if root is not a leaf node.
- **Step 2:** Traverse Left Boundary starting from `root.left`. Add non-leaf node values. Move to `node.left` if available, otherwise fallback to `node.right`.
- **Step 3:** Collect all Leaf Nodes using standard DFS (Preorder/Inorder traversal).
- **Step 4:** Traverse Right Boundary starting from `root.right`. Collect non-leaf node values into a temporary stack/list. Move to `node.right` if available, otherwise fallback to `node.left`.
- **Step 5:** Reverse the collected right boundary nodes and append to the result.

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
    def is_leaf(self, node):
        """Helper to check if a node is a leaf node."""
        return node is not None and node.left is None and node.right is None

    def add_left_boundary(self, root, result):
        """Collects left boundary nodes excluding leaf nodes."""
        curr = root.left
        while curr:
            # Exclude leaf nodes to prevent duplicates
            if not self.is_leaf(curr):
                result.append(curr.val)
            # Edge Case: If left child doesn't exist, move to right child
            if curr.left:
                curr = curr.left
            else:
                curr = curr.right

    def add_leaves(self, root, result):
        """Collects all leaf nodes from left to right using DFS."""
        if not root:
            return
        if self.is_leaf(root):
            result.append(root.val)
            return
        self.add_leaves(root.left, result)
        self.add_leaves(root.right, result)

    def add_right_boundary(self, root, result):
        """Collects right boundary nodes excluding leaf nodes in reverse order."""
        curr = root.right
        temp = []
        while curr:
            # Exclude leaf nodes to prevent duplicates
            if not self.is_leaf(curr):
                temp.append(curr.val)
            # Edge Case: If right child doesn't exist, move to left child
            if curr.right:
                curr = curr.right
            else:
                curr = curr.left

        # Add to result in reverse order (bottom-up)
        for i in range(len(temp) - 1, -1, -1):
            result.append(temp[i])

    def boundaryTraversal(self, root):
        result = []
        if not root:
            return result

        # Step 1: Add root if it is not a leaf node
        if not self.is_leaf(root):
            result.append(root.val)

        # Step 2: Add left boundary
        self.add_left_boundary(root, result)

        # Step 3: Add all leaf nodes
        self.add_leaves(root, result)

        # Step 4: Add right boundary
        self.add_right_boundary(root, result)

        return result
```

---

## Dry Run (Smart Example)

Input Tree: `1` -> Left: `2` (Right child `3`), Right: `4` (Left child `5`)

```
       1
      / \
     2   4
      \ /
      3 5
```

| Step | Variables | Explanation |
| :--- | :--- | :--- |
| 1 | `root = 1`, `result = []` | Root `1` is not leaf. Append `1`. `result = [1]` |
| 2 | `curr = 2` (Left boundary) | `2` is not leaf. Append `2`. `2.left` is None, fallback to `2.right` (`3`). `3` is leaf, loop ends. `result = [1, 2]` |
| 3 | DFS Leaves | Leaf nodes `3` and `5` visited left-to-right. `result = [1, 2, 3, 5]` |
| 4 | `curr = 4` (Right boundary) | `4` is not leaf. `temp = [4]`. `4.right` is None, fallback to `4.left` (`5`). `5` is leaf, loop ends. |
| 5 | Reverse Right Boundary | Reverse `temp` `[4]` and append to `result`. Final: `[1, 2, 3, 5, 4]` |

---

## Edge Cases

- **Single Node Tree:** Root is the only node and a leaf node; return `[root.val]` immediately without duplicate traversal.
- **Skewed Left Tree:** Right boundary is empty; left boundary covers everything except the leaf node.
- **Missing Left Child on Left Boundary:** If `node.left` is missing, traversal must continue via `node.right` to capture outer perimeter.
- **Missing Right Child on Right Boundary:** If `node.right` is missing, traversal must continue via `node.left` to capture outer perimeter.

---

## Mistakes

- **Forget edge cases in `addleft`:** Missing `node.left` means you must route through `node.right` (and vice versa for `addright` routing through `node.left`).
- **Duplicate Leaf Nodes:** Failing to exclude leaf nodes during `addleft` and `addright` causes leaf nodes to be added twice (once in boundary scan, once in leaf scan).
- **Root Duplication:** Adding the root node unconditionally in left/right boundary calls.

---

## Complexity

Time: $O(N)$ → Every node in the tree is visited at most 2 times.
Space: $O(H)$ → $O(N)$ worst-case skew recursion stack space for leaf traversal and auxiliary storage for right boundary.

---

## Similar Problems

- [Binary Tree Right Side View](https://leetcode.com/problems/binary-tree-right-side-view/) - Medium
- [Binary Tree Zigzag Level Order Traversal](https://leetcode.com/problems/binary-tree-zigzag-level-order-traversal/) - Medium
- [Boundary of Binary Tree](https://leetcode.com/problems/boundary-of-binary-tree/) - Medium

---

## Tags and Properties

- #dsa #important #revisit #trees #dfs #recursion
- [[Trees]] [[DFS]] [[Boundary Traversal]]
- **Revision Date:** 2026-09-06
- **Problem Link:** [GeeksforGeeks - Tree Boundary Traversal](https://www.geeksforgeeks.org/problems/boundary-traversal-of-binary-tree/1)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-09-08)
- [ ] Day 7 Revision (2026-09-13)
- [ ] Day 15 Revision (2026-09-21)
- [ ] Day 30 Revision (2026-10-06)
