---
created: 2026-09-04
revisions:
  - 2026-09-06
  - 2026-09-11
  - 2026-09-19
  - 2026-10-04
---

# Diameter Of Binary Tree

---

## Metadata & Placement Tags

- **Folder:** Trees
- **Target Companies:** #Amazon #Facebook #Google #Microsoft #Bloomberg
- **Confidence Checklist:**
  - [ ] Low
  - [ ] Medium
  - [ ] High

- **Concepts:**
  - #dfs [[Depth-First Search]], #tree [[Binary Tree]], #recursion [[Recursion]]

---
## Pattern

Post-Order Traversal (DFS) + Global State Optimization

---
## Difficulty

Easy
#easy

---

## ⚡ Key Idea (Core Insight)

The diameter at any node is `height(left_child) + height(right_child)`. Compute the tree height recursively while updating a global maximum diameter at each node.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Return node height `1 + max(left, right)` to parent, but track diameter `left + right` using a global/instance variable.

---

## Approach

### Brute Force
Calculate `height(left) + height(right)` for every node independently by recomputing tree height at each step.
**Time Complexity:** $O(N^2)$

### Optimal
Use a single bottom-up post-order DFS. For each node, recursively compute the left and right subtree heights, update max diameter (`left + right`), and return height to parent (`1 + max(left, right)`).
**Time Complexity:** $O(N)$

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
    def diameterOfBinaryTree(self, root: TreeNode) -> int:
        self.max_diameter = 0

        def get_height(node: TreeNode) -> int:
            if not node:
                return 0

            # Post-order: process children first
            left_height = get_height(node.left)
            right_height = get_height(node.right)

            # Update global diameter (edges count)
            self.max_diameter = max(self.max_diameter, left_height + right_height)

            # Return height of current subtree
            return 1 + max(left_height, right_height)

        get_height(root)
        return self.max_diameter
```

---

## Dry Run (Smart Example)

Tree structure: `1 -> left: 2 (left: 4, right: 5), right: 3`

| Step | Current Node | Subtree Heights (Left, Right) | Diameter at Node | Max Diameter Updated | Returned Height |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | Leaf `4` | `(0, 0)` | `0 + 0 = 0` | `0` | `1` |
| 2 | Leaf `5` | `(0, 0)` | `0 + 0 = 0` | `0` | `1` |
| 3 | Node `2` | `(1, 1)` | `1 + 1 = 2` | `2` | `2` |
| 4 | Leaf `3` | `(0, 0)` | `0 + 0 = 0` | `2` | `1` |
| 5 | Root `1` | `(2, 1)` | `2 + 1 = 3` | `3` | `3` |

---

## Edge Cases

- **Single Node:** Diameter is `0`.
- **Skewed Tree (Line graph):** Correctly accumulates height down one branch without stack overflow for standard depth.
- **Empty Tree:** Base case returns height `0`, diameter `0`.

---

## Mistakes

- No specific note provided.
- Confusing diameter in terms of **nodes** vs. **edges** (LeetCode expects number of edges).
- Recalculating heights redundantly in $O(N^2)$ instead of carrying max diameter in single traversal.

---

## Complexity

Time: $O(N)$ → Visits every node exactly once.
Space: $O(H)$ → Auxiliary stack space equal to tree height $H$ ($O(N)$ worst case, $O(\log N)$ balanced).

---

## Similar Problems

- [Balanced Binary Tree](https://leetcode.com/problems/balanced-binary-tree/) - Easy
- [Binary Tree Maximum Path Sum](https://leetcode.com/problems/binary-tree-maximum-path-sum/) - Hard
- [Diameter of N-Ary Tree](https://leetcode.com/problems/diameter-of-n-ary-tree/) - Medium

---

## Tags and Properties

- #dsa #important #revisit #dfs #trees
- [[Binary Tree]], [[Depth-First Search]], [[Recursion]]
- **Last Revised:** 2026-09-04
- **Problem Link:** [LeetCode - Diameter of Binary Tree](https://leetcode.com/problems/diameter-of-binary-tree/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-09-06)
- [ ] Day 7 Revision (2026-09-11)
- [ ] Day 15 Revision (2026-09-19)
- [ ] Day 30 Revision (2026-10-04)
