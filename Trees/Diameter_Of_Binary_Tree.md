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
  - #dfs [[Depth-First Search]], #binarytree [[Binary Tree]], #recursion [[Recursion]]

## Pattern

Post-Order Traversal (Bottom-Up DFS)

---
## Difficulty

Easy
#easy

---

## ⚡ Key Idea (Core Insight)

The diameter of a binary tree is the maximum length path between any two nodes, which equals the maximum value of `(left_depth + right_depth)` across all nodes. We compute maximum depths bottom-up using DFS while maintaining a global maximum diameter.

---

## ⚡ Quick Recall (VERY IMPORTANT)

For every node, path length through it = `left_height + right_height`. Return `1 + max(left_height, right_height)` to parent while updating maximum diameter.

---

## Approach

### Brute Force
- Compute height of left and right subtrees for every node separately using recursive `height()` function.
- Time: $O(N^2)$, Space: $O(H)$ where $H$ is tree height.

### Optimal
- Calculate subtree heights in a single bottom-up post-order DFS traversal.
- Update the global maximum diameter `(left_height + right_height)` at each node during recursion.
- Time: $O(N)$, Space: $O(H)$.

---

## Code (Python)

```python
from typing import Optional

class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    def diameterOfBinaryTree(self, root: Optional[TreeNode]) -> int:
        self.max_diameter = 0
        self._calculate_height(root)
        return self.max_diameter

    def _calculate_height(self, node: Optional[TreeNode]) -> int:
        if not node:
            return 0

        # Post-order traversal: process subtrees first
        left_height = self._calculate_height(node.left)
        right_height = self._calculate_height(node.right)

        # Diameter at current node is sum of left and right subtree heights
        self.max_diameter = max(self.max_diameter, left_height + right_height)

        # Return height of subtree rooted at node
        return 1 + max(left_height, right_height)
```

---

## Dry Run (Smart Example)

Input tree: `1` -> left `2`, right `3`. `2` -> left `4`, right `5`.

| Step | Node | Left Height | Right Height | Diameter at Node | Updated Max Diameter | Return Height |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | `4` | 0 | 0 | 0 | 0 | 1 |
| 2 | `5` | 0 | 0 | 0 | 0 | 1 |
| 3 | `2` | 1 | 1 | 2 | 2 | 2 |
| 4 | `3` | 0 | 0 | 0 | 2 | 1 |
| 5 | `1` | 2 | 1 | 3 | 3 | 3 |

---

## Edge Cases

- **Single Node:** Root has no children; diameter is `0`.
- **Skewed Tree (Line graph):** Path goes from root to bottom leaf; height equals recursion depth $O(N)$.
- **Balanced Full Binary Tree:** Max path passes through root node.
- **Diameter Not Passing Through Root:** Longest path exists entirely within a subtree.

---

## Mistakes

- User mistake: No specific note provided.
- Forgetting that diameter is measured by number of **edges**, not number of nodes.
- Re-calculating subtree heights redundantly inside helper calls ($O(N^2)$ mistake).
- Assuming the longest path must pass through the root node.

---

## Complexity

Time: $O(N)$ → Visits every node exactly once during DFS traversal.
Space: $O(H)$ → Call stack depth proportional to tree height ($O(\log N)$ for balanced, $O(N)$ for skewed).

---

## Similar Problems

- [Balanced Binary Tree](https://leetcode.com/problems/balanced-binary-tree/) - Easy
- [Binary Tree Maximum Path Sum](https://leetcode.com/problems/binary-tree-maximum-path-sum/) - Hard
- [Diameter of N-Ary Tree](https://leetcode.com/problems/diameter-of-n-ary-tree/) - Medium
- [Longest Path With Different Adjacent Characters](https://leetcode.com/problems/longest-path-with-different-adjacent-characters/) - Hard

---

## Tags and Properties

- #dsa #important #revisit #dfs #binarytree
- Concepts: [[Binary Tree]], [[Depth-First Search]], [[Recursion]]
- Revision Date: 2026-09-04
- **Problem Link:** [Diameter of Binary Tree - LeetCode](https://leetcode.com/problems/diameter-of-binary-tree/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-09-06)
- [ ] Day 7 Revision (2026-09-11)
- [ ] Day 15 Revision (2026-09-19)
- [ ] Day 30 Revision (2026-10-04)
