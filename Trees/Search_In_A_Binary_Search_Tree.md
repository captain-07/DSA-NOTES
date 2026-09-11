---
created: 2026-09-11
revisions:
  - 2026-09-13
  - 2026-09-18
  - 2026-09-26
  - 2026-10-11
---

# Search In A Binary Search Tree

---

## Metadata & Placement Tags

- **Folder:** Trees
- **Target Companies:** #Amazon #Microsoft #Google #Adobe #Meta
- **Confidence Checklist:**
  - [ ] Low
  - [ ] Medium
  - [ ] High

- **Concepts:**
  - #bst [[Binary Search Tree]], #trees [[Tree Search]], #iteration [[Iterative BST Traversal]]

## Pattern

Binary Search Tree Search (Divide & Conquer / Elimination)

---
## Difficulty

Easy
Tag: #easy

---

## ⚡ Key Idea (Core Insight)

- Leverage the **BST property**: values in left subtree < `val`, values in right subtree > `val`.
- At each node, compare `val` with node's value to eliminate half of the remaining search space.

---

## ⚡ Quick Recall (VERY IMPORTANT)

- Traverse down: go `left` if `val < root.val`, go `right` if `val > root.val`, stop when `root` matches or is `None`.

---

## Approach

### Brute Force
- Perform a standard Tree Traversal (DFS/BFS) without using BST properties, searching every node.
- Time: $O(N)$ | Space: $O(N)$ stack space.

### Optimal
1. Start at the `root`.
2. While `curr` node is not `None` and `curr.val != val`:
   - If `val < curr.val`, move to `curr.left`.
   - Else, move to `curr.right`.
3. Return `curr` (either the matching node or `None`).

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
    def searchBST(self, root: TreeNode, val: int) -> TreeNode:
        curr = root

        # Traverse the tree using BST property iteratively
        while curr is not None and curr.val != val:
            if val < curr.val:
                curr = curr.left   # Target is smaller, go to left subtree
            else:
                curr = curr.right  # Target is larger, go to right subtree

        return curr
```

---

## Dry Run (Smart Example)

Input: `root = [4, 2, 7, 1, 3]`, `val = 2`

| Step | Variables | Explanation |
| :--- | :--- | :--- |
| 1 | `curr = Node(4)` | `4 != 2`. Target `2 < 4`, move to `curr.left`. |
| 2 | `curr = Node(2)` | `2 == 2`. Loop terminates. |
| 3 | Return `curr` | Returns reference to node with value `2`. |

---

## Edge Cases

- `root` is `None`: Returns `None` immediately.
- `val` not present in BST: Iterates until `curr` becomes `None` and returns `None`.
- `val` is at `root`: Loop condition fails immediately, returns `root`.
- Single-node tree (match/no-match): Correctly handles both in 1 step.

---

## Mistakes

- Using recursion instead of iteration; **iterative approach is better** because it saves $O(H)$ memory by operating in $O(1)$ auxiliary space.
- Not checking if `root` is `None` before accessing `root.val`.
- Treating the tree as a binary tree instead of taking advantage of BST properties.

---

## Complexity

Time: $O(H)$ → where $H$ is tree height ($O(\log N)$ average, $O(N)$ worst-case skew tree).
Space: $O(1)$ → iterative traversal requires no call stack or extra memory.

---

## Similar Problems

- [Insert into a Binary Search Tree](https://leetcode.com/problems/insert-into-a-binary-search-tree/) - Medium
- [Delete Node in a BST](https://leetcode.com/problems/delete-node-in-a-bst/) - Medium
- [Lowest Common Ancestor of a Binary Search Tree](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-search-tree/) - Medium

---

## Tags and Properties

- #dsa #important #revisit #bst #trees
- [[Binary Search Tree]] [[Iterative Traversal]]
- **Revision Date:** 2026-09-11
- **Problem Link:** [Search in a Binary Search Tree - LeetCode](https://leetcode.com/problems/search-in-a-binary-search-tree/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-09-13)
- [ ] Day 7 Revision (2026-09-18)
- [ ] Day 15 Revision (2026-09-26)
- [ ] Day 30 Revision (2026-10-11)
