---
created: 2026-08-31
revisions:
  - 2026-09-02
  - 2026-09-07
  - 2026-09-15
  - 2026-09-30
---

# Traversal Of Binary Tree Recursive

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Google #Microsoft #Meta #Adobe

- **Confidence Checklist:**
  - [ ] Low
  - [ ] Medium
  - [ ] High

- **Concepts:**
  - #binarytree [[Binary Tree]], #dfs [[Depth First Search]]

## Pattern
Tree DFS

---
## Difficulty
Easy
#easy

---
## ⚡ Key Idea (Core Insight)

The traversal order (preorder, inorder, postorder) is defined by when the current (root) node is visited relative to its left and right subtrees:
- **Preorder:** **Root** -> Left -> Right
- **Inorder:** Left -> **Root** -> Right
- **Postorder:** Left -> Right -> **Root**

---
## ⚡ Quick Recall (VERY IMPORTANT)

Associate the prefix with the root's position: **Pre** means root is first, **In** means root is in the middle, **Post** means root is at the end.

---
## Approach

### Brute Force
N/A (Standard recursive traversal is already optimal for visiting all nodes).
Time: O(N)

### Better
Iterative DFS using a stack to avoid recursion stack overhead.
Time: O(N), Space: O(N)

### Optimal
Recursive DFS traversal (standard) or Morris Traversal for O(1) auxiliary space (by modifying tree pointers).
Time: O(N), Space: O(H) where H is tree height.

---
## Code (Python)

```python
# Definition for a binary tree node.
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    # 1. Preorder Traversal (Root -> Left -> Right)
    def preorderTraversal(self, root: TreeNode) -> list[int]:
        res = []
        def dfs(node):
            if not node:
                return
            res.append(node.val) # Root
            dfs(node.left)       # Left
            dfs(node.right)      # Right
        dfs(root)
        return res

    # 2. Inorder Traversal (Left -> Root -> Right)
    def inorderTraversal(self, root: TreeNode) -> list[int]:
        res = []
        def dfs(node):
            if not node:
                return
            dfs(node.left)       # Left
            res.append(node.val) # Root
            dfs(node.right)      # Right
        dfs(root)
        return res

    # 3. Postorder Traversal (Left -> Right -> Root)
    def postorderTraversal(self, root: TreeNode) -> list[int]:
        res = []
        def dfs(node):
            if not node:
                return
            dfs(node.left)       # Left
            dfs(node.right)      # Right
            res.append(node.val) # Root
        dfs(root)
        return res
```

---
## Dry Run (Smart Example)

Input tree:
```
    1
   / \
  2   3
```

### Dry Run for Inorder Traversal (Left -> Root -> Right)

| Step | Variables | Explanation |
| :--- | :--- | :--- |
| 1 | `node = 1` | DFS(1) initiated. Traverses to left child. |
| 2 | `node = 2` | DFS(2) initiated. DFS(2.left) is null. Appends `2`. DFS(2.right) is null. Returns to node 1. |
| 3 | `node = 1` | DFS(1.left) finished. Appends `1`. Traverses to DFS(1.right). |
| 4 | `node = 3` | DFS(3) initiated. DFS(3.left) is null. Appends `3`. DFS(3.right) is null. Returns. |

Result: `[2, 1, 3]`

---
## Edge Cases

- **Empty Tree (root is None):** Should immediately return `[]`.
- **Single Node Tree:** Returns a list containing just the single node value.
- **Skewed Tree (All left or all right nodes):** Verifies correct recursion depth handling.

---
## Mistakes

- Confusing the order of visiting node: Pre (Root-Left-Right), In (Left-Root-Right), Post (Left-Right-Root).
- Forgetting the base case `if not node: return` leading to infinite recursion.
- Modifying the result list out of order when translating recursive logic to iterative.

---
## Complexity

Time: O(N) → Each node is visited exactly once.
Space: O(H) → Recursion stack space is proportional to tree height H (worst case O(N) for skewed tree, best case O(log N)).

---
## Similar Problems

- [Binary Tree Inorder Traversal](https://leetcode.com/problems/binary-tree-inorder-traversal/) - Easy
- [Binary Tree Preorder Traversal](https://leetcode.com/problems/binary-tree-preorder-traversal/) - Easy
- [Binary Tree Postorder Traversal](https://leetcode.com/problems/binary-tree-postorder-traversal/) - Easy
- [Binary Tree Level Order Traversal](https://leetcode.com/problems/binary-tree-level-order-traversal/) - Medium

---
## Tags and Properties

- #dsa #important #revisit
- #binarytree [[Binary Tree]] #dfs [[Depth First Search]]
- **Revision Date:** 2026-08-31
- **Problem Link:** [LeetCode - Binary Tree Inorder Traversal](https://leetcode.com/problems/binary-tree-inorder-traversal/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-09-02)
- [ ] Day 7 Revision (2026-09-07)
- [ ] Day 15 Revision (2026-09-15)
- [ ] Day 30 Revision (2026-09-30)
