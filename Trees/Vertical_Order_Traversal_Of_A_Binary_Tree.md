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
  - #trees [[Trees]], #bfs [[BFS]], #dfs [[DFS]], #hashmap [[HashMap]], #sorting [[Sorting]]

## Pattern

BFS / DFS + Coordinate Tracking (Row, Column) + Sorting

---
## Difficulty

Hard #hard

---

## ⚡ Key Idea (Core Insight)

- Assign `(row, col)` coordinates to each node: root is `(0, 0)`. Left child gets `(row + 1, col - 1)` and right child gets `(row + 1, col + 1)`.
- Group nodes by `col`, then by `row`, and sort nodes at the same `(row, col)` position by value in ascending order.

---

## ⚡ Quick Recall (VERY IMPORTANT)

- Track `(node, row, col)` using BFS/DFS. Map `col -> row -> list of node values`. Sort `col` keys, `row` keys, and values at equal coordinates.

---

## Approach

### Brute Force
- Store all nodes in a list with `(row, col, value)` via traversal. Sort the list primary by `col`, secondary by `row`, tertiary by `value`. Group into output.
- Time Complexity: O(N log N) | Space Complexity: O(N)

### Optimal
- Use BFS queue storing `(node, row, col)` to traverse tree layer by layer.
- Maintain a hash map: `nodes[col][row] = [values]`.
- Keep track of `min_col` and `max_col` to avoid sorting column keys. Sort only the `row` keys and values at matching `(col, row)`.

---

## Code (Python)

```python
from collections import deque, defaultdict

# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-09-09)
- [ ] Day 7 Revision (2026-09-14)
- [ ] Day 15 Revision (2026-09-22)
- [ ] Day 30 Revision (2026-10-07)
