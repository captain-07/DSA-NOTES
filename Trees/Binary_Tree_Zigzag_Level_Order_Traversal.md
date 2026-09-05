---
created: 2026-09-05
revisions:
  - 2026-09-07
  - 2026-09-12
  - 2026-09-20
  - 2026-10-05
---

# Binary Tree Zigzag Level Order Traversal

---

## Metadata & Placement Tags

- **Folder:** Trees
- **Target Companies:** #Amazon #Microsoft #Google #Meta #Bloomberg
- **Confidence Checklist:**
  - [ ] Low
  - [ ] Medium
  - [ ] High

- **Concepts:**
  - #tree [[Trees]], #bfs [[Breadth-First Search]], #queue [[Queue]], #bitmanipulation [[Bit Manipulation]]

## Pattern

BFS (Breadth-First Search) Level-Order Traversal + Direction Flag Switch

---
## Difficulty

Medium
Tag: #medium

---

## ⚡ Key Idea (Core Insight)

Standard BFS level-order traversal using a queue. Track level direction using an alternating flag (`flag = 1` for left-to-right, `0` for right-to-left). Alternate the flag at each level using bitwise XOR (`flag ^= 1`) and reverse level results when needed (or insert accordingly).

---

## ⚡ Quick Recall (VERY IMPORTANT)

Standard BFS level order traversal; use `flag ^= 1` to alternate direction at each level.

---

## Approach

### Brute Force
- Perform DFS/BFS, collect all nodes with level depth indices into an array, and reverse odd-indexed level arrays at the end.
- Time: O(N), Space: O(N)

### Optimal
- Use standard queue-based BFS level order traversal.
- Maintain a `flag` initialized to `1` (left-to-right).
- Process nodes level by level. If `flag == 0`, reverse the level array before appending to the final result.
- Toggle direction after each level using `flag ^= 1`.
- Time: O(N), Space: O(N)

---

## Code (Python)

```python
from collections import deque
from typing import List, Optional

# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right

class Solution:
    def zigzagLevelOrder(self, root: Optional['TreeNode']) -> List[List[int]]:
        if not root:
            return []

        result = []
        queue = deque([root])
        # flag = 1 indicates left-to-right, flag = 0 indicates right-to-left
        flag = 1

        while queue:
            level_size = len(queue)
            current_level = []

            for _ in range(level_size):
                node = queue.popleft()
                current_level.append(node.val)

                # Add child nodes to the queue for next level
                if node.left:
                    queue.append(node.left)
                if node.right:
                    queue.append(node.right)

            # If flag is 0, reverse current level for right-to-left order
            if flag == 0:
                current_level.reverse()

            result.append(current_level)

            # Alternate flag using bitwise XOR (1 -> 0 -> 1)
            flag ^= 1

        return result
```

---

## Dry Run (Smart Example)

Tree: `[3, 9, 20, null, null, 15, 7]`

| Step | Queue | `flag` | Level Nodes | Action / `current_level` | `result` |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | `[3]` | `1` | `[3]` | Normal order (`flag==1`), `flag ^= 1` -> `0` | `[[3]]` |
| 2 | `[9, 20]` | `0` | `[9, 20]` | Reversed order (`flag==0`) -> `[20, 9]`, `flag ^= 1` -> `1` | `[[3], [20, 9]]` |
| 3 | `[15, 7]` | `1` | `[15, 7]` | Normal order (`flag==1`), `flag ^= 1` -> `0` | `[[3], [20, 9], [15, 7]]` |

---

## Edge Cases

- **Empty Tree (`root = None`):** Returns empty list `[]`.
- **Single Node Tree:** Returns `[[val]]` without error.
- **Skewed Tree (Left or Right only):** Correctly alternates single-element levels.

---

## Mistakes

- Forgetting to alternate direction at each level iteration.
- The flag is variable main part using bitwise operation (`flag ^= 1`) to alternate it amazing rest same as level order traversal.
- Reversing queue nodes instead of level values.

---

## Complexity

Time: O(N) → Visits each node exactly once and reverses level array of max size N.
Space: O(N) → Queue holds at most maximum width of tree (O(N) nodes).

---

## Similar Problems

- [Binary Tree Level Order Traversal](https://leetcode.com/problems/binary-tree-level-order-traversal/) - Medium
- [Binary Tree Level Order Traversal II](https://leetcode.com/problems/binary-tree-level-order-traversal-ii/) - Medium
- [Populating Next Right Pointers in Each Node](https://leetcode.com/problems/populating-next-right-pointers-in-each-node/) - Medium

---

## Tags and Properties

- #dsa #important #revisit #trees #bfs #queue
- [[Trees]] [[Breadth-First Search]] [[Queue]] [[Bit Manipulation]]
- **Revision Date:** 2026-09-05
- **Problem Link:** [LeetCode - Binary Tree Zigzag Level Order Traversal](https://leetcode.com/problems/binary-tree-zigzag-level-order-traversal/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-09-07)
- [ ] Day 7 Revision (2026-09-12)
- [ ] Day 15 Revision (2026-09-20)
- [ ] Day 30 Revision (2026-10-05)
