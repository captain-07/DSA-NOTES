---
created: 2026-09-17
revisions:
  - 2026-09-19
  - 2026-09-24
  - 2026-10-02
  - 2026-10-17
---

# Lowest Common Ancestor Of A Binary Search Tree

---

## Metadata & Placement Tags

- **Folder:** Trees
- **Target Companies:** #Amazon #Microsoft #Google #Facebook #Apple
- **Confidence Checklist:**
  - [ ] Low
  - [ ] Medium
  - [x] High

- **Concepts:**
  - #bst [[Binary Search Tree]], #trees [[Trees]], #recursion [[Recursion]], #depthfirstsearch [[DFS]]

## Pattern

Binary Search Tree Property (Split Point / BST Traversal)

---
## Difficulty

Easy
#easy

---

## ⚡ Key Idea (Core Insight)

- Leverage the BST property (`left < root < right`).
- Starting from root: if both nodes `p` and `q` are smaller, search left; if both are larger, search right.
- The **first node** where `p` and `q` split (one is smaller, one is larger) or where root equals `p` or `q` is the Lowest Common Ancestor.

---

## ⚡ Quick Recall (VERY IMPORTANT)

- Walk down the tree: if both `p, q < curr`, go left; if both `p, q > curr`, go right; else `curr` is the LCA.

---

## Approach

### Brute Force
- Find paths from root to `p` and root to `q` using generic binary tree DFS. Compare paths to find last common node.
- Time: $O(N)$, Space: $O(N)$ for storing paths.

### Optimal (Iterative BST Traversal)
- Step 1: Start at `curr = root`.
- Step 2: Loop while `curr` is not None.
- Step 3: If `p.val < curr.val` and `q.val < curr.val`, move `curr = curr.left`.
- Step 4: Else if `p.val > curr.val` and `q.val > curr.val`, move `curr = curr.right`.
- Step 5: Else, `curr` is the split point, return `curr`.

---

## Code (Python)

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def lowestCommonAncestor(self, root: 'TreeNode', p: 'TreeNode', q: 'TreeNode') -> 'TreeNode':
        current = root

        while current:
            # If both p and q are smaller than current, LCA is in left subtree
            if p.val < current.val and q.val < current.val:
                current = current.left
            # If both p and q are greater than current, LCA is in right subtree
            elif p.val > current.val and q.val > current.val:
                current = current.right
            # We found the split point (or one of the nodes equals current)
            else:
                return current

        return None
```

---

## Dry Run (Smart Example)

**Input Tree:** `root = [6,2,8,0,4,3,5]`, `p = 2`, `q = 4`

| Step | `current.val` | Condition Check | Explanation |
| :--- | :--- | :--- | :--- |
| 1 | `6` | `p(2) < 6` and `q(4) < 6` | Both nodes are smaller than root, move to `current.left`. |
| 2 | `2` | `p(2) <= 2` and `q(4) > 2` | Split detected (`p.val == current.val`). Return node `2`. |

---

## Edge Cases

- **One node is ancestor of the other (`p = 2, q = 4` where `2` is parent of `4`):** Split condition handles this as `p.val == curr.val`.
- **`p` and `q` are on opposite subtrees of root:** Directly returns root at step 1.
- **Skewed tree (LinkedList-like BST):** Traverses sequentially until target split.

---

## Mistakes

- Treating it as a generic Binary Tree and building root-to-node path arrays.
- Forgetting that equal value (`p.val == curr.val` or `q.val == curr.val`) means current node is the LCA.
- User mistake: very easy just have to know the logic.

---

## Complexity

Time: $O(H) \rightarrow O(\log N)$ on balanced BST, $O(N)$ worst-case for skewed tree.
Space: $O(1) \rightarrow$ Iterative approach uses constant extra memory.

---

## Similar Problems

- [Lowest Common Ancestor of a Binary Tree](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree/) - Medium
- [Smallest Common Region](https://leetcode.com/problems/smallest-common-region/) - Medium
- [Lowest Common Ancestor of Deepest Leaves](https://leetcode.com/problems/lowest-common-ancestor-of-deepest-leaves/) - Medium

---

## Tags and Properties

- #dsa #important #revisit
- #bst #binarysearchtree #lca
- [[Binary Search Tree]], [[Trees]], [[Lowest Common Ancestor]]
- **Revision Date:** 2026-09-17
- **Problem Link:** [Lowest Common Ancestor of a Binary Search Tree - LeetCode](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-search-tree/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-09-19)
- [ ] Day 7 Revision (2026-09-24)
- [ ] Day 15 Revision (2026-10-02)
- [ ] Day 30 Revision (2026-10-17)
