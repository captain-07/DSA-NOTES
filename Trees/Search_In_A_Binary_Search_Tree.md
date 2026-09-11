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
- **Target Companies:** #Amazon #Microsoft #Google #Adobe
- **Confidence Checklist:**
  - [ ] Low
  - [ ] Medium
  - [x] High

- **Concepts:**
  - #binarysearchtree [[Binary Search Tree]], #trees [[Trees]], #iteration [[Iteration]]

---
## Pattern

Binary Search Tree Traversal / Binary Search Logic

---
## Difficulty

Easy
#easy

---

## ⚡ Key Idea (Core Insight)

Leverage the BST property: for any node, all left subtree values are smaller and all right subtree values are larger. Traverse left if `target < node.val`, right if `target > node.val`, and return the node if `target == node.val`.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Iterate using standard BST binary search logic (`curr = curr.left` or `curr = curr.right`) until `curr` is null or `curr.val == val`.

---

## Approach

### Brute Force
- Traverse every node in the tree using DFS/BFS ignoring BST properties.
- Time: $O(N)$, Space: $O(N)$

### Optimal (Iterative)
- Start at the root node.
- Use a `while` loop while `root` is not `None` and `root.val != val`.
- Move `root` to `root.left` if `val < root.val`, else move to `root.right`.
- Return `root` (either the matching node or `None`).

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
        # Traverse the BST iteratively using BST property
        current_node = root

        while current_node is not None and current_node.val != val:
            if val < current_node.val:
                current_node = current_node.left
            else:
                current_node = current_node.right

        return current_node
```

---

## Dry Run (Smart Example)

Input: `root = [4,2,7,1,3]`, `val = 2`

| Step | Variables | Explanation |
| :--- | :--- | :--- |
| 1 | `current_node = Node(4)` | `4 != 2` and `2 < 4`, so move to `left` |
| 2 | `current_node = Node(2)` | `2 == 2`, while loop condition `current_node.val != val` fails |
| 3 | `current_node = Node(2)` | Loop terminates. Return `current_node` |

---

## Edge Cases

- **Empty Tree (`root = None`):** Returns `None` immediately without error.
- **Value Not Present:** Returns `None` after reaching a leaf's child (`None`).
- **Target at Root:** Loop condition fails immediately, returns `root`.
- **Target is a Leaf Node:** Correctly traverses down to leaf and returns it.

---

## Mistakes

- Using a recursive approach: iterative approach is better because it avoids call stack overhead ($O(1)$ auxiliary space vs $O(H)$).
- Treating it like a general binary tree and exploring both left and right subtrees.
- Not handling the case where `val` is not present in the BST (causes `AttributeError` if checking `.val` on `None`).

---

## Complexity

Time: $O(H)$ where $H$ is the height of the BST ($O(\log N)$ average, $O(N)$ worst-case skew tree) — eliminates subtrees at each step.
Space: $O(1)$ — iterative search uses no extra call stack memory.

---

## Similar Problems

- [Insert into a Binary Search Tree](https://leetcode.com/problems/insert-into-a-binary-search-tree/) - Medium
- [Delete Node in a BST](https://leetcode.com/problems/delete-node-in-a-bst/) - Medium
- [Validate Binary Search Tree](https://leetcode.com/problems/validate-binary-search-tree/) - Medium

---

## Tags and Properties

- #dsa #important #revisit
- #bst #binarytree #trees
- [[Binary Search Tree]] [[Tree Traversal]]
- **Revision Date:** 2026-09-11
- **Problem Link:** [Search in a Binary Search Tree - LeetCode](https://leetcode.com/problems/search-in-a-binary-search-tree/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-09-13)
- [ ] Day 7 Revision (2026-09-18)
- [ ] Day 15 Revision (2026-09-26)
- [ ] Day 30 Revision (2026-10-11)
