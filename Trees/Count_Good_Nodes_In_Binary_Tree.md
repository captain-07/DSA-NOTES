---
created: 2026-10-24
revisions:
  - 2026-10-26
  - 2026-10-31
  - 2026-11-08
  - 2026-11-23
---

# Count Good Nodes in Binary Tree

---

## Metadata & Placement Tags

- **Folder:** Trees
- **Target Companies:** #Microsoft #Amazon #Google #Facebook
- **Confidence Checklist:**
  - [ ] Low
  - [ ] Medium
  - [ ] High

- **Concepts:**
  - #dfs [[Depth-First Search]], #trees [[Binary Tree]], #recursion [[Recursion]]

## Pattern

Tree Traversal (DFS with Running Maximum)

---
## Difficulty

Medium
#medium

---

## ⚡ Key Idea (Core Insight)

A node is "good" if its value is greater than or equal to the maximum value seen on the path from the root to that node. Track `max_so_far` while traversing down the tree.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Pre-order DFS: pass `max(max_so_far, node.val)` to child recursive calls; increment count if `node.val >= max_so_far`.

---

## Approach

### Brute Force
- For every node, traverse back up to the root to verify no ancestor has a greater value.
- Time: $O(N^2)$ in a skewed tree.

### Better
- Store path nodes in an array/list during DFS and check `max(path)` at each step.
- Time: $O(N \cdot H)$ where $H$ is tree height.

### Optimal
1. Start DFS from root with `max_so_far = root.val`.
2. At each node, check if `node.val >= max_so_far`. If true, count it as a good node.
3. Update `new_max = max(max_so_far, node.val)`.
4. Recursively traverse left and right children passing `new_max`, summing valid counts.

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
    def _count_good_nodes(self, node: TreeNode, max_so_far: int) -> int:
        if not node:
            return 0

        # Check if the current node is "good"
        good_count = 0
        if node.val >= max_so_far:
            good_count = 1

        # Update the maximum value seen along this path
        current_max = max(max_so_far, node.val)

        # Recursively count good nodes in left and right subtrees
        good_count += self._count_good_nodes(node.left, current_max)
        good_count += self._count_good_nodes(node.right, current_max)

        return good_count

    def goodNodes(self, root: TreeNode) -> int:
        if not root:
            return 0
        # Root is always good, start with its own value as max_so_far
        return self._count_good_nodes(root, root.val)
```

---

## Dry Run (Smart Example)

Input: `root = [3, 1, 4, 3, null, 1, 5]`

| Step | Node (`node.val`) | `max_so_far` | Condition (`val >= max_so_far`) | Action / Next Step |
| :--- | :--- | :--- | :--- | :--- |
| 1 | `3` (Root) | `3` | `3 >= 3` (True) | Count = 1, recurse left with max `3` |
| 2 | `1` (Left child) | `3` | `1 >= 3` (False) | Count = 0, recurse left child `3` with max `3` |
| 3 | `3` (Left-Left) | `3` | `3 >= 3` (True) | Count = 1, leaves return 0. Subtree sum = 1 |
| 4 | `4` (Right child) | `3` | `4 >= 3` (True) | Count = 1, recurse left (`1`, max `4`), right (`5`, max `4`) |
| 5 | `5` (Right-Right) | `4` | `5 >= 4` (True) | Count = 1, leaf node. Total good nodes = 4 |

---

## Edge Cases

- **Single Node:** Only root exists; output is always `1`.
- **All Strictly Decreasing Values:** (e.g., `5 -> 4 -> 3`); only root is counted (`1`).
- **All Identical Values:** (e.g., `3 -> 3 -> 3`); every node satisfies `>=` and is counted.
- **Negative Values:** Tree with negative numbers (e.g., `[-3, -5, -1]`); ensure `max_so_far` is initialized to `root.val`, not `0`.

---

## Mistakes

- User Mistake: No specific note provided.
- Initializing `max_so_far` to `0` instead of `root.val` or `-infinity`, failing when node values are negative.
- Using strict greater-than (`>`) instead of greater-than-or-equal-to (`>=`).
- Mutating a global maximum instead of scoping `max_so_far` to the current recursion path.

---

## Complexity

Time: O(N) → Visits each node in the tree exactly once.
Space: O(H) → Recursive call stack equals the height of the tree ($O(\log N)$ best, $O(N)$ worst).

---

## Similar Problems

- [Path Sum](https://leetcode.com/problems/path-sum/) - Easy
- [Binary Tree Maximum Path Sum](https://leetcode.com/problems/binary-tree-maximum-path-sum/) - Hard
- [Longest Univalue Path](https://leetcode.com/problems/longest-univalue-path/) - Medium
- [Step-By-Step Directions From a Binary Tree Node to Another](https://leetcode.com/problems/step-by-step-directions-from-a-binary-tree-node-to-another/) - Medium

---

## Tags and Properties

- #dsa #important #revisit
- #binarytree #dfs [[Depth-First Search]] [[Binary Tree]]
- **Revision Date:** 2026-10-24
- **Problem Link:** [LeetCode: Count Good Nodes in Binary Tree](https://leetcode.com/problems/count-good-nodes-in-binary-tree/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-10-26)
- [ ] Day 7 Revision (2026-10-31)
- [ ] Day 15 Revision (2026-11-08)
- [ ] Day 30 Revision (2026-11-23)
