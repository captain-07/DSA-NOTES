---
created: 2026-09-02
revisions:
  - 2026-09-04
  - 2026-09-09
  - 2026-09-17
  - 2026-10-02
---

# Binary Tree Level Order Traversal

---

## Metadata & Placement Tags

- **Target Companies:** #Amazon #Microsoft #Google #Meta #Apple
- **Confidence Checklist:**
  - [ ] Low
  - [ ] Medium
  - [ ] High
- **Concepts:** #bfs [[Breadth-First Search]], #tree [[Tree]], #queue [[Queue]]

---

## Pattern

BFS (Breadth-First Search) + Level-by-Level Queue Processing

---

## Difficulty

Medium | #medium

---

## ⚡ Key Idea (Core Insight)

Use a **Queue (FIFO)** to process nodes level by level. At the start of each level iteration, snapshot the queue's size (`len(queue)`). This fixed size determines exactly how many nodes belong to the current level before popping them and pushing their child nodes.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Level order traversal == BFS using Queue. Lock level size with `len(queue)` at each level loop to separate tree levels.

---

## Approach

### Brute Force
- Perform DFS to traverse all nodes, keeping track of depth/level, and group node values into an array indexed by level.
- **Time:** O(N) | **Space:** O(H) recursion stack where H is tree height.

### Optimal
- Use a `collections.deque` queue.
- Push `root` into queue.
- While queue is non-empty:
  1. Capture current size `level_size = len(queue)`.
  2. Iterate `level_size` times: pop node from front, append value to current level list, push left/right children to queue.
  3. Append level list to main result list.

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
    def levelOrder(self, root: Optional[TreeNode]) -> List[List[int]]:
        if not root:
            return []

        result = []
        queue = deque([root])

        while queue:
            level_size = len(queue)
            current_level = []

            for _ in range(level_size):
                node = queue.popleft()
                current_level.append(node.val)

                if node.left:
                    queue.append(node.left)
                if node.right:
                    queue.append(node.right)

            result.append(current_level)

        return result
```

---

## Dry Run (Smart Example)

Tree: `[3, 9, 20, null, null, 15, 7]`

| Step | Queue State (Node Vals) | Variables (`level_size`, `current_level`) | Explanation |
| :--- | :--- | :--- | :--- |
| **1** | `[3]` | `level_size=1`, `current_level=[]` | Initial state. Process root level. |
| **2** | `[9, 20]` | `level_size=1`, `current_level=[3]` | Pop `3`, push children `9` & `20`. Level 0 complete. |
| **3** | `[15, 7]` | `level_size=2`, `current_level=[9, 20]` | Pop `9` & `20`, push children `15` & `7`. Level 1 complete. |
| **4** | `[]` | `level_size=2`, `current_level=[15, 7]` | Pop `15` & `7`, no children. Level 2 complete. Queue empty. |

---

## Edge Cases

- **Empty Tree (`root = None`):** Return `[]` directly.
- **Single Node Tree:** Output `[[val]]`.
- **Skewed Tree (Left/Right heavy):** Handles gracefully; acts like a single element per level.
- **Complete / Full Binary Tree:** Evenly spreads memory across leaf level.

---

## Mistakes

- Using a queue is interesting—it's actually standard **BFS**; tree level traversal inherently relies on queue FIFO ordering.
- Forgetting to fix/snapshot `len(queue)` at start of level loop, leading to mixing adjacent levels together.
- Forgetting to check if `root` is `None` before pushing to queue.

---

## Complexity

Time: O(N) → Every node is visited and processed exactly once.
Space: O(N) → Queue stores at most max leaf nodes at bottom level (up to N/2 nodes).

---

## Similar Problems

- [Binary Tree Zigzag Level Order Traversal](https://leetcode.com/problems/binary-tree-zigzag-level-order-traversal/) - Medium
- [Binary Tree Level Order Traversal II](https://leetcode.com/problems/binary-tree-level-order-traversal-ii/) - Medium
- [Average of Levels in Binary Tree](https://leetcode.com/problems/average-of-levels-in-binary-tree/) - Easy
- [Binary Tree Right Side View](https://leetcode.com/problems/binary-tree-right-side-view/) - Medium

---

## Tags and Properties

- #dsa #important #revisit #bfs #binarytree
- [[Breadth-First Search]] [[Binary Tree]] [[Queue]]
- **Last Revised:** 2026-09-02
- **Problem Link:** [Binary Tree Level Order Traversal - LeetCode](https://leetcode.com/problems/binary-tree-level-order-traversal/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-09-04)
- [ ] Day 7 Revision (2026-09-09)
- [ ] Day 15 Revision (2026-09-17)
- [ ] Day 30 Revision (2026-10-02)
