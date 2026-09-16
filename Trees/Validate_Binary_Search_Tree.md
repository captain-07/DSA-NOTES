---
created: 2026-09-16
revisions:
  - 2026-09-18
  - 2026-09-23
  - 2026-10-01
  - 2026-10-16
---

# Validate Binary Search Tree

---

## Metadata & Placement Tags

- **Folder:** Trees
- **Target Companies:** #Amazon #Google #Microsoft #Facebook #Bloomberg #Apple
- **Confidence Checklist:**
  - [ ] Low
  - [ ] Medium
  - [ ] High

- **Concepts:** #bst [[Binary Search Tree]], #recursion [[Recursion]], #dfs [[DFS]], #inorder [[Inorder Traversal]]

## Pattern

DFS with Range Boundaries / Inorder Traversal Validation

---
## Difficulty

Medium
#medium

---

## ⚡ Key Idea (Core Insight)

Checking `node.left.val < node.val < node.right.val` locally is NOT enough because deep descendant nodes can violate ancestors' constraints. Instead, carry a valid range `(low, high)` down the recursion: every node must satisfy `low < node.val < high`. When moving left, update `high = node.val`; when moving right, update `low = node.val`.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Pass valid boundaries `(low, high)` down the tree. Left child inherits current `low` and upper limit becomes `node.val`. Right child inherits current `high` and lower limit becomes `node.val`.

---

## Approach

### Brute Force
- Perform Inorder Traversal to collect elements into an array, then check if the array is strictly sorted.
- Time: O(N), Space: O(N) auxiliary array storage.

### Optimal 1: Recursive Range / Constraint Validation (Top-Down DFS)
1. Pass `low` and `high` bounds starting as `(-inf, +inf)`.
2. Base case: If node is `None`, return `True`.
3. If `node.val <= low` or `node.val >= high`, return `False`.
4. Recursively validate left subtree with `(low, node.val)` and right subtree with `(node.val, high)`.

### Optimal 2: Inorder Traversal (Iterative / Recursive with Previous Pointer)
1. Perform an in-order traversal (Left, Root, Right).
2. Keep track of `prev_val`.
3. Each visited node's value must be strictly greater than `prev_val`.

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
    def isValidBST(self, root: TreeNode) -> bool:
        # Range validation approach (DFS)
        return self._validate(root, float('-inf'), float('inf'))

    def _validate(self, node: TreeNode, low: float, high: float) -> bool:
        # Base case: An empty node/tree is a valid BST
        if not node:
            return True

        # Current node value must strictly be within (low, high) range
        if node.val <= low or node.val >= high:
            return False

        # Left child must be < node.val; Right child must be > node.val
        left_valid = self._validate(node.left, low, node.val)
        right_valid = self._validate(node.right, node.val, high)

        return left_valid and right_valid
```

---

## Dry Run (Smart Example)

Invalid BST Tree: `[10, 5, 15, null, null, 6, 20]` (Node 6 is right child of 15, but violates 10 < 6).

| Step | Current Node & Range | Action / Condition | Result |
| :--- | :--- | :--- | :--- |
| 1 | `node = 10`, `(-inf, inf)` | `-inf < 10 < inf` (Valid). Recurse Left & Right. | Pending |
| 2 | `node = 5`, `(-inf, 10)` | `-inf < 5 < 10` (Valid). Left/Right are `None`. | Returns `True` |
| 3 | `node = 15`, `(10, inf)` | `10 < 15 < inf` (Valid). Recurse Left `(10, 15)`. | Pending |
| 4 | `node = 6`, `(10, 15)` | `6 <= 10` (Fails condition `low < node.val`). | Returns `False` |

---

## Edge Cases

- **Single Node Tree:** Valid (`True`).
- **Duplicate Values (`node.val == low` or `high`):** Invalid (`False`), BST requires strictly `<` and `>`.
- **Integer Limits (`INT_MIN`, `INT_MAX` node values):** Initial range must be `(-inf, inf)`, not standard int bounds.
- **Deep Left/Right skew:** Handled correctly by boundary updates.

---

## Mistakes

- Only checking immediate children (`node.left < node` and `node.right > node`) without propagating ancestor constraints.
- **User Mistake:** Finding the concept of using a range to validate a node mind-boggling. *Mental Pivot:* Think of bounds as "ancestor walls". Going left erects a ceiling (upper bound); going right erects a floor (lower bound).
- Using `<=` or `>=` instead of strict `<` and `>`.

---

## Complexity

Time: O(N) → Visits each node exactly once.
Space: O(H) → Recursive call stack depth, where H is height of tree (O(N) worst case, O(log N) balanced).

---

## Similar Problems

- [Validate Binary Search Tree](https://leetcode.com/problems/validate-binary-search-tree/) - Medium
- [Search in a Binary Search Tree](https://leetcode.com/problems/search-in-a-binary-search-tree/) - Easy
- [Kth Smallest Element in a BST](https://leetcode.com/problems/kth-smallest-element-in-a-bst/) - Medium
- [Lowest Common Ancestor of a Binary Search Tree](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-search-tree/) - Medium

---

## Tags and Properties

- #dsa #important #revisit
- #binarytree #dfs #recursion
- [[Binary Search Tree]], [[Depth-First Search]], [[Tree Traversal]]
- **Last Revised:** 2026-09-16
- **Problem Link:** [LeetCode - Validate Binary Search Tree](https://leetcode.com/problems/validate-binary-search-tree/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-09-18)
- [ ] Day 7 Revision (2026-09-23)
- [ ] Day 15 Revision (2026-10-01)
- [ ] Day 30 Revision (2026-10-16)
