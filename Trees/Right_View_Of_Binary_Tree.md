---
created: 2026-09-08
revisions:
  - 2026-09-10
  - 2026-09-15
  - 2026-09-23
  - 2026-10-08
---

# Right View Of Binary Tree

---

## Metadata & Placement Tags

- **Folder:** Trees
- **Target Companies:** #Amazon #Facebook #Google #Microsoft #Bloomberg
- **Confidence Checklist:**
  - [ ] Low
  - [ ] Medium
  - [ ] High

- **Concepts:** #bfs [[BFS]], #dfs [[DFS]], #binarytree [[Binary Tree]]

---
## Pattern

Level Order Traversal (BFS) / Preorder Traversal Variation (DFS)

---
## Difficulty

Medium #medium

---

## ⚡ Key Idea (Core Insight)

The right view contains the **last node at each depth/level**.
- **BFS (Iterative):** Traverse level by level queue-wise; record the last element of each level.
- **DFS (Recursive):** Traverse `Root -> Right -> Left`, tracking current depth; the first node visited at any new depth belongs to the right view.

---

## ⚡ Quick Recall (VERY IMPORTANT)

- **Iterative (BFS):** Standard level-order traversal, append the last node's value in the level queue.
- **Recursive (DFS):** `Root -> Right -> Left` traversal; append to result if `depth == len(result)`.

---

## Approach

### Brute Force
- Store all nodes along with their level and horizontal position in a map using level-order traversal, then extract the rightmost node per level.
- **Time Complexity:** $O(N \log N)$ or $O(N)$ with heavy space overhead.

### Optimal 1: Iterative (BFS Level Order)
- Process tree level by level using a queue.
- For each level, loop through its size. If it's the last iteration in the loop (rightmost node), append its value to the result.

### Optimal 2: Recursive (DFS Reverse Preorder)
- Traverse nodes in `Root -> Right -> Left` order.
- Maintain `current_depth`. If `current_depth == len(result)`, this is the first time reaching this level from the right side, so add node value to result.

---

## Code (Python)

```python
from collections import deque
from typing import List, Optional

# Definition for a binary tree node.
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    def rightSideView_Iterative(self, root: Optional[TreeNode]) -> List[int]:
        """Iterative BFS Approach using Queue"""
        if not root:
            return []

        result = []
        queue = deque([root])

        while queue:
            level_size = len(queue)

            for i in range(level_size):
                curr_node = queue.popleft()

                # If it's the last node of the current level, append to result
                if i == level_size - 1:
                    result.append(curr_node.val)

                # Add child nodes for the next level
                if curr_node.left:
                    queue.append(curr_node.left)
                if curr_node.right:
                    queue.append(curr_node.right)

        return result

    def rightSideView_Recursive(self, root: Optional[TreeNode]) -> List[int]:
        """Recursive DFS Approach using Root -> Right -> Left"""
        result = []
        self._dfs(root, 0, result)
        return result

    def _dfs(self, node: Optional[TreeNode], depth: int, result: List[int]) -> None:
        if not node:
            return

        # If visiting this depth for the first time, it's the rightmost node
        if depth == len(result):
            result.append(node.val)

        # Prioritize right subtree first
        self._dfs(node.right, depth + 1, result)
        self._dfs(node.left, depth + 1, result)
```

---

## Dry Run (Smart Example)

Input Tree: `[1, 2, 3, null, 5, null, 4]`

```text
      1
    /   \
   2     3
    \     \
     5     4
```

| Step | Current State (DFS) | Explanation |
| :--- | :--- | :--- |
| 1 | `node = 1, depth = 0, res = []` | `depth == len(res)` (0 == 0) $\rightarrow$ append `1`. `res = [1]` |
| 2 | `node = 3, depth = 1, res = [1]` | Go Right: `depth == len(res)` (1 == 1) $\rightarrow$ append `3`. `res = [1, 3]` |
| 3 | `node = 4, depth = 2, res = [1, 3]` | Go Right: `depth == len(res)` (2 == 2) $\rightarrow$ append `4`. `res = [1, 3, 4]` |
| 4 | `node = 2, depth = 1, res = [1, 3, 4]` | Backtrack & Go Left: `depth < len(res)` (1 < 3) $\rightarrow$ skip `2`. |
| 5 | `node = 5, depth = 2, res = [1, 3, 4]` | Go Right of 2: `depth < len(res)` (2 < 3) $\rightarrow$ skip `5`. |

---

## Edge Cases

- **Empty Tree (`root = None`):** Return `[]`.
- **Single Node:** Return `[root.val]`.
- **Left Skewed Tree:** Should return all nodes from root to leaf.
- **Right Skewed Tree:** Should return all nodes from root to leaf.

---

## Mistakes

- Using standard DFS `Root -> Left -> Right` instead of `Root -> Right -> Left` for recursive approach.
- Forgetting to show both recursive (DFS) and iterative (BFS) approaches in interviews.
- For BFS: Not tracking `level_size` before the inner loop, leading to level mixing.

---

## Complexity

- **Time:** $O(N)$ → Visits every node exactly once in both BFS and DFS.
- **Space:** $O(H)$ for DFS where $H$ is tree height (recursion stack); $O(W)$ for BFS where $W$ is maximum width of tree (queue size). Worst case $O(N)$.

---

## Similar Problems

- [Binary Tree Right Side View](https://leetcode.com/problems/binary-tree-right-side-view/) - Medium
- [Binary Tree Left Side View](https://practice.geeksforgeeks.org/problems/left-view-of-binary-tree/1) - Easy
- [Binary Tree Level Order Traversal](https://leetcode.com/problems/binary-tree-level-order-traversal/) - Medium

---

## Tags and Properties

- #dsa #important #revisit #trees #bfs #dfs
- [[BFS]] [[DFS]] [[Binary Tree]]
- **Problem Link:** [LeetCode - Binary Tree Right Side View](https://leetcode.com/problems/binary-tree-right-side-view/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-09-10)
- [ ] Day 7 Revision (2026-09-15)
- [ ] Day 15 Revision (2026-09-23)
- [ ] Day 30 Revision (2026-10-08)
