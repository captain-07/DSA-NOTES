---
created: 2026-09-07
revisions:
  - 2026-09-09
  - 2026-09-14
  - 2026-09-22
  - 2026-10-07
---

# Vertical Order Traversal Of A Binary Tree

---

## Metadata & Placement Tags

- **Folder:** Trees
- **Target Companies:** #Amazon #Google #Microsoft #Facebook #Bloomberg
- **Confidence Checklist:**
  - [ ] Low
  - [ ] Medium
  - [ ] High

- **Concepts:**
  - #bfs [[Breadth-First Search]], #dfs [[Depth-First Search]], #hashtable [[Hash Table]], #sorting [[Sorting]], #tree [[Binary Tree]]

## Pattern

BFS / DFS + Coordinate Tracking (Col, Row) + Sorting / Map

---
## Difficulty

Hard
#hard

---

## ⚡ Key Idea (Core Insight)

- Assign coordinates `(col, row)` to each node: root is `(0, 0)`, left child is `(col - 1, row + 1)`, right child is `(col + 1, row + 1)`.
- Group nodes by column index `col`. For nodes with the same `(col, row)`, sort them by value in ascending order.

---

## ⚡ Quick Recall (VERY IMPORTANT)

- Track `(node, col, row)` using BFS/DFS, map nodes to `nodes[col][row]`, then sort columns and row buckets.

---

## Approach

### Brute Force
- Recursively collect all node coordinates into a flat list `[(col, row, val)]`, then sort the list by `col` ascending, `row` ascending, `val` ascending.
- Time Complexity: $O(N \log N)$
- Space Complexity: $O(N)$

### Optimal
- Use BFS with a queue storing `(node, col, row)` to traverse level-by-level (keeps `row` naturally ordered).
- Store nodes in a nested hashmap/dictionary `nodes[col][row] = list_of_vals` while maintaining `min_col` and `max_col`.
- Iterate `col` from `min_col` to `max_col`, sort values at the same `(col, row)`, and append to final result.
- Time Complexity: $O(N \log(N/k))$ where $k$ is the number of unique columns.
- Space Complexity: $O(N)$

---

## Code (Python)

```python
from collections import defaultdict, deque

# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right

class Solution:
    def verticalTraversal(self, root: TreeNode) -> list[list[int]]:
        if not root:
            return []

        # Dictionary structure: nodes[col][row] = list of node values
        nodes = defaultdict(lambda: defaultdict(list))

        # Queue for BFS storing tuples: (node, col, row)
        queue = deque([(root, 0, 0)])

        min_col = 0
        max_col = 0

        while queue:
            curr_node, col, row = queue.popleft()

            # Store current node value at specific col and row
            nodes[col][row].append(curr_node.val)

            # Track column bounds to avoid sorting column keys later
            min_col = min(min_col, col)
            max_col = max(max_col, col)

            # Traverse left child: col decreases, row increases
            if curr_node.left:
                queue.append((curr_node.left, col - 1, row + 1))

            # Traverse right child: col increases, row increases
            if curr_node.right:
                queue.append((curr_node.right, col + 1, row + 1))

        result = []

        # Build output column by column from left to right
        for col in range(min_col, max_col + 1):
            col_nodes = []
            # Iterate through rows in ascending order
            for row in sorted(nodes[col].keys()):
                # Sort values if multiple nodes exist at the exact same (col, row)
                col_nodes.extend(sorted(nodes[col][row]))
            result.append(col_nodes)

        return result
```

---

## Dry Run (Smart Example)

Input Tree: `[1, 2, 3, 4, 6, 5, 7]` where node `6` and `5` collide at `col=0, row=2`.

| Step | Queue / Processing | State (`nodes[col][row]`) | Explanation |
| :--- | :--- | :--- | :--- |
| 1 | Pop `(1, col=0, row=0)` | `nodes[0][0] = [1]` | Push left `(2, -1, 1)` and right `(3, 1, 1)` |
| 2 | Pop `(2, col=-1, row=1)` | `nodes[-1][1] = [2]` | Push left `(4, -2, 2)` and right `(6, 0, 2)` |
| 3 | Pop `(3, col=1, row=1)` | `nodes[1][1] = [3]` | Push left `(5, 0, 2)` and right `(7, 2, 2)` |
| 4 | Pop `(6, col=0, row=2)` & `(5, col=0, row=2)` | `nodes[0][2] = [6, 5]` | Collision at `col=0, row=2`. Will be sorted to `[5, 6]` in output step. |

---

## Edge Cases

- **Single Node Tree:** Output `[[val]]`.
- **Skewed Tree (Left/Right):** Each node gets its own column.
- **Multiple Overlapping Nodes at Same `(col, row)`:** Values must be sorted numerically, not by insertion order.

---

## Mistakes

- Forgetting to sort nodes that share both the exact same column AND row.
- Confusing vertical traversal with simple top-view or bottom-view binary tree problems.
- User mistake: No specific note provided.

---

## Complexity

Time: $O(N \log (N/K))$ → Traversing tree takes $O(N)$, sorting nodes within small row buckets takes $O(K \log K)$ where $K \ll N$.
Space: $O(N)$ → Hashmap and queue store all $N$ nodes in memory.

---

## Similar Problems

- [Binary Tree Vertical Order Traversal](https://leetcode.com/problems/binary-tree-vertical-order-traversal/) - Medium
- [Binary Tree Zigzag Level Order Traversal](https://leetcode.com/problems/binary-tree-zigzag-level-order-traversal/) - Medium
- [Top View of Binary Tree](https://practice.geeksforgeeks.org/problems/top-view-of-binary-tree/1) - Medium

---

## Tags and Properties

- #dsa #important #revisit
- #binarytree #col-row-coordinates #tree-traversal
- [[Binary Tree]], [[Breadth-First Search]], [[Sorting]]
- **Revision Date:** 2026-09-07
- **Problem Link:** [LeetCode - Vertical Order Traversal of a Binary Tree](https://leetcode.com/problems/vertical-order-traversal-of-a-binary-tree/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-09-09)
- [ ] Day 7 Revision (2026-09-14)
- [ ] Day 15 Revision (2026-09-22)
- [ ] Day 30 Revision (2026-10-07)
