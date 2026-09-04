---
created: 2026-09-04
revisions:
  - 2026-09-06
  - 2026-09-11
  - 2026-09-19
  - 2026-10-04
---

# Maximum Depth In Bt

---

## Metadata & Placement Tags

- **Folder:** Trees
- **Target Companies:** #Amazon #Google #Microsoft #Facebook #Apple
- **Confidence Checklist:**
  - [ ] Low
  - [ ] Medium
  - [ ] High
- **Concepts:** #binarytree [[Binary Tree]], #dfs [[Depth First Search]], #bfs [[Breadth First Search]], #recursion [[Recursion]]

## Pattern

DFS / Recursion (Bottom-up) OR BFS (Level Order Traversal)

---
## Difficulty

Easy
#easy

---

## ⚡ Key Idea (Core Insight)

The max depth of a binary tree rooted at node `root` is `1 + max(depth(root.left), depth(root.right))`. Base case: empty node has depth 0.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Depth = 1 + max(left_depth, right_depth) recursively, or count levels via queue BFS.

---

## Approach

### Brute Force
- Traversal of all root-to-leaf paths storing path lengths, then taking the maximum.
- Time: O(N) | Space: O(N) (for storing path arrays)

### Optimal 1: Recursive DFS (Post-order)
1. Base case: If node is `None`, return 0.
2. Recursively find left subtree depth and right subtree depth.
3. Return `1 + max(left, right)`.

### Optimal 2: Iterative BFS (Level Order)
1. Use a queue initialized with `root`.
2. Process level by level using queue size; increment depth counter for each level.

---

## Code (Python)

```python
from typing import Optional
from collections import deque

# Definition for a binary tree node.
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    def maxDepth(self, root: Optional[TreeNode]) -> int:
        # Approach 1: Recursive DFS
        if not root:
            return 0

        left_depth = self.maxDepth(root.left)
        right_depth = self.maxDepth(root.right)

        return 1 + max(left_depth, right_depth)

    def maxDepth_BFS(self, root: Optional[TreeNode]) -> int:
        # Approach 2: Iterative BFS
        if not root:
            return 0

        queue = deque([root])
        depth = 0

        while queue:
            depth += 1
            for _ in range(len(queue)):
                node = queue.popleft()
                if node.left:
                    queue.append(node.left)
                if node.right:
                    queue.append(node.right)

        return depth
```

---

## Dry Run (Smart Example)

Input: `[3, 9, 20, null, null, 15, 7]`

| Step | Variables | Explanation |
| :--- | :--- | :--- |
| 1 | `node=15/7` | Base leaves return 1 to parent 20. |
| 2 | `node=20` | Left depth=1, Right depth=1 $\rightarrow$ Returns $1 + \max(1, 1) = 2$. |
| 3 | `node=9` | Leaf node $\rightarrow$ Returns 1. |
| 4 | `node=3` | Left depth=1, Right depth=2 $\rightarrow$ Returns $1 + \max(1, 2) = 3$. |

---

## Edge Cases

- `root = None`: Returns 0.
- Single node tree: Returns 1.
- Skewed tree (linked list structure): Correctly calculates depth $N$.
- Balanced full tree: Correctly calculates depth $\log N$.

---

## Mistakes

- Forgetting base case `if not root: return 0` causing `AttributeError`.
- Confusing height (1-indexed vs 0-indexed edges); problem requires node count.
- User mistake: No specific note provided.

---

## Complexity

Time: O(N) $\rightarrow$ Visits every node exactly once.
Space: O(H) $\rightarrow$ Call stack space proportional to height $H$ (O(N) worst case, O(log N) best case).

---

## Similar Problems

- [Minimum Depth of Binary Tree](https://leetcode.com/problems/minimum-depth-of-binary-tree/) - Easy
- [Balanced Binary Tree](https://leetcode.com/problems/balanced-binary-tree/) - Easy
- [Diameter of Binary Tree](https://leetcode.com/problems/diameter-of-binary-tree/) - Easy

---

## Tags and Properties

- #dsa #important #revisit
- #binarytree #dfs #recursion [[Binary Tree]] [[Depth First Search]]
- **Revision Date:** 2026-09-04
- **Problem Link:** [Maximum Depth of Binary Tree](https://leetcode.com/problems/maximum-depth-of-binary-tree/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-09-06)
- [ ] Day 7 Revision (2026-09-11)
- [ ] Day 15 Revision (2026-09-19)
- [ ] Day 30 Revision (2026-10-04)
