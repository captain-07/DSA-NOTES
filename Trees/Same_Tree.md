---
created: 2026-09-05
revisions:
  - 2026-09-07
  - 2026-09-12
  - 2026-09-20
  - 2026-10-05
---

# Same Tree

---

## Metadata & Placement Tags

- **Folder:** Trees
- **Target Companies:** #Amazon #Google #Microsoft #Facebook #Apple #LinkedIn

- **Confidence Checklist:**
  - [ ] Low
  - [ ] Medium
  - [x] High

- **Concepts:**
  - #trees [[Trees]], #dfs [[Depth First Search]], #recursion [[Recursion]], #binarytree [[Binary Tree]]

## Pattern

Tree DFS / Preorder Traversal

---
## Difficulty

Easy #easy

---

## ⚡ Key Idea (Core Insight)

- Two trees are identical if their root values are equal and both their left and right subtrees are structural and value-wise identical.
- Check nodes recursively in a preorder fashion (root, left, right).

---

## ⚡ Quick Recall (VERY IMPORTANT)

- Base case clean trick: `if not p or not q: return p == q`. Then check `p.val == q.val` and recursively call on left and right subtrees.

---

## Approach

### Brute Force
- Convert both binary trees to serialized string representations (e.g., preorder listing with null placeholders) and compare the two strings.
- Time: O(N), Space: O(N)

### Optimal (Recursive DFS)
1. Check base cases for null nodes: if either node is `None`, return whether both are `None`.
2. Check value equality: if `p.val != q.val`, return `False`.
3. Recursively check if `p.left` matches `q.left` AND `p.right` matches `q.right`.

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
    def isSameTree(self, p: TreeNode, q: TreeNode) -> bool:
        # Base case: if either node is None, they are identical only if both are None
        if not p or not q:
            return p == q

        # Check current node values and recursively validate left and right subtrees
        if p.val != q.val:
            return False

        return self.isSameTree(p.left, q.left) and self.isSameTree(p.right, q.right)
```

---

## Dry Run (Smart Example)

Input: `p = [1, 2]`, `q = [1, null, 2]`

| Step | Variables (`p`, `q`) | Explanation |
|---|---|---|
| 1 | `p=Node(1)`, `q=Node(1)` | Neither is None. `p.val == q.val` (1 == 1). Proceed to check subtrees. |
| 2 | `p=Node(2)`, `q=None` (left children) | `q` is None. Evaluate `not p or not q` -> True. Return `p == q` -> `False`. |
| 3 | Final Result | Left subtree comparison returned `False`, short-circuits and returns `False`. |

---

## Edge Cases

- **Both trees empty (`p = None, q = None`):** Returns `True` via `p == q`.
- **One tree empty (`p = Node(1), q = None`):** Returns `False` via `p == q`.
- **Different structure, same values:** Structural failure caught when one node is `None` while the other is not.
- **Same structure, different values:** Value check `p.val != q.val` catches discrepancy immediately.

---

## Mistakes

- Explicitly writing 3 different `if` conditions for null checks (`if not p and not q`, `if not p or not q`) instead of using the concise base case: `if not p or not q: return p == q` which handles all base case scenarios cleanly.
- Forgetting to compare `p.val` before calling recursive helper.

---

## Complexity

Time: O(N) → Must visit every node once in the worst case (where N is the minimum number of nodes in the two trees).
Space: O(H) → Call stack space bounded by tree height H (O(N) for degenerate skewed tree, O(log N) for balanced tree).

---

## Similar Problems

- [Symmetric Tree](https://leetcode.com/problems/symmetric-tree/) - Easy
- [Subtree of Another Tree](https://leetcode.com/problems/subtree-of-another-tree/) - Easy
- [Flip Equivalent Binary Trees](https://leetcode.com/problems/flip-equivalent-binary-trees/) - Medium

---

## Tags and Properties

- #dsa #important #revisit
- #binarytree [[Binary Tree]] #dfs [[Depth First Search]]
- **Revision Date:** 2026-09-05
- **Problem Link:** [LeetCode - Same Tree](https://leetcode.com/problems/same-tree/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-09-07)
- [ ] Day 7 Revision (2026-09-12)
- [ ] Day 15 Revision (2026-09-20)
- [ ] Day 30 Revision (2026-10-05)
