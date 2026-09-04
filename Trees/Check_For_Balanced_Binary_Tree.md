---
created: 2026-09-04
revisions:
  - 2026-09-06
  - 2026-09-11
  - 2026-09-19
  - 2026-10-04
---

# Check For Balanced Binary Tree

---

## Metadata & Placement Tags

- **Folder:** Trees
- **Target Companies:** #Amazon #Google #Microsoft #Facebook #Bloomberg
- **Confidence Checklist:**
  - [ ] Low
  - [ ] Medium
  - [ ] High

- **Concepts:** #binarytree [[Binary Tree]], #dfs [[Depth First Search]], #recursion [[Recursion]], #tree-depth [[Tree Depth]]

## Pattern

DFS / Post-order Traversal (Bottom-Up)

---
## Difficulty

Easy | #easy

---

## ⚡ Key Idea (Core Insight)

Use bottom-up DFS (post-order traversal) to calculate heights of left and right subtrees. If any subtree is unbalanced ($|height_{left} - height_{right}| > 1$), return `-1` to propagate the failure immediately up the call stack.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Bottom-up post-order DFS: return `-1` early when height difference between left and right subtrees exceeds 1; otherwise return `1 + max(left_h, right_h)`.

---

## Approach

### Brute Force
Compute the height of left and right subtrees at every node using top-down recursion. Recomputes node heights repeatedly.
**Time:** $O(N^2)$ | **Space:** $O(H)$

### Optimal
Bottom-up post-order DFS. Check balance status at subtrees before returning height to parent. If a child returns `-1`, immediately return `-1`.
1. Base case: Null node has height `0`.
2. Recursively get height of left subtree; if `-1`, return `-1`.
3. Recursively get height of right subtree; if `-1`, return `-1`.
4. If $|height_{left} - height_{right}| > 1$, return `-1`.
5. Return `1 + max(height_{left}, height_{right})`.
**Time:** $O(N)$ | **Space:** $O(H)$

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
    def isBalanced(self, root: Optional[TreeNode]) -> bool:
        def check_height(node: Optional[TreeNode]) -> int:
            # Empty nodes are balanced with height 0
            if not node:
                return 0

            left_h = check_height(node.left)
            if left_h == -1:
                return -1  # Left subtree unbalanced

            right_h = check_height(node.right)
            if right_h == -1:
                return -1  # Right subtree unbalanced

            # Check balance condition for current node
            if abs(left_h - right_h) > 1:
                return -1

            return 1 + max(left_h, right_h)

        return check_height(root) != -1
```

---

## Dry Run (Smart Example)

Input tree: `[1, 2, 2, 3, 3, null, null, 4, 4]` (Unbalanced skewed tree)

| Step | Node | Variables | Explanation |
| :--- | :--- | :--- | :--- |
| 1 | Leaf node `4` | `left_h=0, right_h=0` | $|0-0| \le 1$, returns height `1` |
| 2 | Node `3` (left child of 2) | `left_h=1 (node 4), right_h=0` | $|1-0| \le 1$, returns height `2` |
| 3 | Node `2` (left child of 1) | `left_h=2 (node 3), right_h=0` | $|2-0| = 2 > 1$, condition fails! Returns `-1` |
| 4 | Root node `1` | `left_h=-1` | Early exit triggered; returns `-1` -> Tree is unbalanced (`False`) |

---

## Edge Cases

- **Empty Tree (`root = None`):** Returns `True` (height 0).
- **Single Node (`root = TreeNode(1)`):** Returns `True` (height 1).
- **Completely Skewed Tree (Linked list structure):** Evaluates imbalance at shallowest node, returning `False` early.
- **Perfectly Balanced Tree:** Traverses all nodes and returns `True`.

---

## Mistakes

- User mistake: No specific note provided.
- Computing height top-down resulting in inefficient $O(N^2)$ time complexity.
- Forgetting to check if subtree already returned `-1` before doing height check.
- Returning `abs(left - right)` instead of `1 + max(left, right)` for valid heights.

---

## Complexity

- **Time:** $O(N)$ → Each node visited at most once in post-order traversal.
- **Space:** $O(H)$ → Recursion stack height, where $H$ is tree height ($O(\log N)$ balanced, $O(N)$ worst-case).

---

## Similar Problems

- [Maximum Depth of Binary Tree](https://leetcode.com/problems/maximum-depth-of-binary-tree/) - Easy
- [Minimum Depth of Binary Tree](https://leetcode.com/problems/minimum-depth-of-binary-tree/) - Easy
- [Diameter of Binary Tree](https://leetcode.com/problems/diameter-of-binary-tree/) - Easy
- [Balanced Binary Tree](https://leetcode.com/problems/balanced-binary-tree/) - Easy

---

## Tags and Properties

- #dsa #important #revisit #trees #dfs [[Binary Tree]] [[Depth First Search]]
- **Revision Date:** 2026-09-04
- **Problem Link:** [LeetCode - Balanced Binary Tree](https://leetcode.com/problems/balanced-binary-tree/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-09-06)
- [ ] Day 7 Revision (2026-09-11)
- [ ] Day 15 Revision (2026-09-19)
- [ ] Day 30 Revision (2026-10-04)
