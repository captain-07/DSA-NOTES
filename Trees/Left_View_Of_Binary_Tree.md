---
created: 2026-09-08
revisions:
  - 2026-09-10
  - 2026-09-15
  - 2026-09-23
  - 2026-10-08
---

# Left View Of Binary Tree

---

## Metadata & Placement Tags

- **Folder:** Trees
- **Target Companies:** #Amazon #Flipkart #Oyo #Paytm #Samsung
- **Confidence Checklist:**
  - [ ] Low
  - [ ] Medium
  - [ ] High

- **Concepts:**
  - #trees [[Trees]], #bfs [[Breadth First Search]], #dfs [[Depth First Search]], #recursion [[Recursion]]

## Pattern

BFS Level Order Traversal OR Preorder DFS (Root -> Left -> Right)

---
## Difficulty

Medium
Tag: #medium

---

## ⚡ Key Idea (Core Insight)

- The left view consists of the first node visible at each level when looking from the left side.
- **BFS:** Process level by level, picking the first element of each queue snapshot.
- **DFS:** Track current depth/level; visit Root -> Left -> Right and insert the node into result only when `level == len(result)`.

---

## ⚡ Quick Recall (VERY IMPORTANT)

- BFS: First node of every level queue iteration.
- DFS: Preorder `(Root, Left, Right)` + insert node when `depth == len(ans)`.

---

## Approach

### Brute Force
- Store full level-order traversal of all nodes in a 2D array and extract the 0th index from each sub-array.
- Time: O(N), Space: O(N)

### Better
- N/A (BFS / DFS are already optimal for full tree traversal)

### Optimal

**Approach 1: Iterative (BFS / Level Order)**
1. Use a queue for standard Level Order Traversal.
2. At each level, note the level size `k`.
3. The first node processed in that level (`i == 0`) is part of the left view.

**Approach 2: Recursive (DFS / Modified Preorder)**
1. Traverse using Preorder `(Root -> Left -> Right)`.
2. Pass `current_level` starting from `0`.
3. If `current_level == len(result)`, this is the first time we visit this level, so append the node's value.

---

## Code (Python)

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right

from collections import deque

class Solution:
    # -------------------------------------------------------------
    # Approach 1: Iterative (BFS Level Order Traversal)
    # -------------------------------------------------------------
    def leftViewIterative(self, root: TreeNode) -> list[int]:
        if not root:
            return []

        result = []
        queue = deque([root])

        while queue:
            level_size = len(queue)

            for i in range(level_size):
                current_node = queue.popleft()

                # The first node of each level belongs to the left view
                if i == 0:
                    result.append(current_node.val)

                # Push left child first, then right child
                if current_node.left:
                    queue.append(current_node.left)
                if current_node.right:
                    queue.append(current_node.right)

        return result

    # -------------------------------------------------------------
    # Approach 2: Recursive (DFS Modified Preorder Traversal)
    # -------------------------------------------------------------
    def leftViewRecursive(self, root: TreeNode) -> list[int]:
        result = []
        self._dfs(root, 0, result)
        return result

    def _dfs(self, node: TreeNode, current_level: int, result: list[int]) -> None:
        if not node:
            return

        # If visiting this level for the first time, add to result
        if current_level == len(result):
            result.append(node.val)

        # Prioritize Left node first to ensure left view visibility
        self._dfs(node.left, current_level + 1, result)
        self._dfs(node.right, current_level + 1, result)
```

---

## Dry Run (Smart Example)

**Input Tree:** `[1, 2, 3, None, 5, 4, None]`
Structure:
```text
     1
   /   \
  2     3
   \   /
    5 4
```

| Step | Current Node / State | Action / Explanation | Result Array |
| :--- | :--- | :--- | :--- |
| 1 | Node 1 (Level 0) | First node at Level 0 → Append 1. Recurse Left (Node 2). | `[1]` |
| 2 | Node 2 (Level 1) | First node at Level 1 (`1 == len(result)`) → Append 2. Recurse Left (None), then Right (Node 5). | `[1, 2]` |
| 3 | Node 5 (Level 2) | First node at Level 2 (`2 == len(result)`) → Append 5. Leaves return. | `[1, 2, 5]` |
| 4 | Node 3 (Level 1) | Level 1 visited already (`1 < len(result)`). Recurse Left (Node 4). | `[1, 2, 5]` |
| 5 | Node 4 (Level 2) | Level 2 visited already (`2 < len(result)`). Skip. Return. | `[1, 2, 5]` |

---

## Edge Cases

- **Empty Tree (`root = None`):** Should return `[]`.
- **Single Node Tree:** Returns `[root.val]`.
- **Right-skewed Tree:** Left view contains all nodes (since right nodes become visible when no left nodes exist).
- **Left-skewed Tree:** Returns all left-most nodes down the tree.

---

## Mistakes

- Only considering left children instead of the first node at each level (right child might be visible if no left child exists at a level).
- **User Mistake:** Preparing only one approach in interview — always know both iterative (BFS) and recursive (DFS) solutions.
- In DFS, traversing right child before left child (this produces Right View instead).

---

## Complexity

Time: O(N) → Visits every node exactly once.
Space: O(H) for DFS call stack / O(W) for BFS queue, where H is height and W is maximum width of tree. Worst case O(N).

---

## Similar Problems

- [Binary Tree Right Side View](https://leetcode.com/problems/binary-tree-right-side-view/) - Medium
- [Binary Tree Level Order Traversal](https://leetcode.com/problems/binary-tree-level-order-traversal/) - Medium
- [Find Bottom Left Tree Value](https://leetcode.com/problems/find-bottom-left-tree-value/) - Medium

---

## Tags and Properties

- #dsa #important #revisit
- #binarytree #leftview #bfs #dfs
- [[Binary Tree]], [[Breadth First Search]], [[Depth First Search]]
- **Revision Date:** 2026-09-08
- **Problem Link:** [GeeksforGeeks - Left View of Binary Tree](https://www.geeksforgeeks.org/problems/left-view-of-binary-tree/1)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-09-10)
- [ ] Day 7 Revision (2026-09-15)
- [ ] Day 15 Revision (2026-09-23)
- [ ] Day 30 Revision (2026-10-08)
