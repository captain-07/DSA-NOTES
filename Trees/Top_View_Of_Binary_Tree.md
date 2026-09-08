---
created: 2026-09-08
revisions:
  - 2026-09-10
  - 2026-09-15
  - 2026-09-23
  - 2026-10-08
---

# Top View Of Binary Tree

---

## Metadata & Placement Tags

- **Folder:** Trees
- **Target Companies:** #Amazon #Microsoft #Paytm #Walmart #Flipkart
- **Confidence Checklist:**
  - [ ] Low
  - [ ] Medium
  - [ ] High

- **Concepts:**
  - #tree [[Trees]], #bfs [[Breadth First Search]], #hashmap [[HashMap]], #queue [[Queue]]

## Pattern

BFS (Level Order Traversal) + Vertical Line Coordinate System (HashMap)

---
## Difficulty

Medium
Tag: #medium

---

## ⚡ Key Idea (Core Insight)

- Assign a horizontal distance (HD) to each node: root is 0, left child is `hd - 1`, right child is `hd + 1`.
- Perform level order traversal (BFS). The first node encountered at each unique horizontal distance is the top-most node visible for that vertical column.

---

## ⚡ Quick Recall (VERY IMPORTANT)

- Use BFS with Queue `(node, hd)` + Map `hd -> node.val`. Only insert into Map if `hd` is seen for the first time!

---

## Approach

### Brute Force
- Perform DFS to find the min and max horizontal distances, then for each distance from min to max, find the top-most node by checking levels.
- Time: O(N^2) | Space: O(N)

### Optimal
- Use BFS with a Queue storing tuples of `(node, hd)` and a Hash Map storing `hd -> node.val`.
- Queue ensures we process upper levels before lower levels. The first entry stored for each HD is guaranteed to be the top view node.
- Time: O(N log N) if map is sorted or O(N) using min/max track | Space: O(N)

---

## Code (Python)

```python
from collections import deque

class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    def topView(self, root: TreeNode) -> list[int]:
        if not root:
            return []

        # Hash map to store the first node value at each horizontal distance (hd)
        top_node_map = {}

        # Queue for BFS: stores tuples of (node, horizontal_distance)
        queue = deque([(root, 0)])

        min_hd = 0
        max_hd = 0

        while queue:
            current_node, hd = queue.popleft()

            # Record min and max hd to avoid sorting map keys later
            min_hd = min(min_hd, hd)
            max_hd = max(max_hd, hd)

            # If hd is seen for the first time, this is the top view node for this column
            if hd not in top_node_map:
                top_node_map[hd] = current_node.val

            # Process left child with hd - 1
            if current_node.left:
                queue.append((current_node.left, hd - 1))

            # Process right child with hd + 1
            if current_node.right:
                queue.append((current_node.right, hd + 1))

        # Construct result array from min_hd to max_hd
        result = []
        for line in range(min_hd, max_hd + 1):
            result.append(top_node_map[line])

        return result
```

---

## Dry Run (Smart Example)

Input Tree: `[1, 2, 3, null, 4, null, 5]`
Structure:
```text
      1 (hd=0)
     / \
(hd=-1) 2   3 (hd=1)
     \   \
  (hd=0) 4   5 (hd=2)
```

| Step | Queue Content | HashMap (`hd: val`) | Explanation |
| :--- | :--- | :--- | :--- |
| 1 | `[(1, 0)]` | `{}` | Start BFS at root node 1 (HD=0). |
| 2 | `[(2, -1), (3, 1)]` | `{0: 1}` | Pop `(1,0)`. Add `0:1` to map. Push left `(2,-1)` and right `(3,1)`. |
| 3 | `[(3, 1), (4, 0)]` | `{0: 1, -1: 2}` | Pop `(2,-1)`. Add `-1:2` to map. Push right child `(4,0)`. |
| 4 | `[(4, 0), (5, 2)]` | `{0: 1, -1: 2, 1: 3}` | Pop `(3,1)`. Add `1:3` to map. Push right child `(5,2)`. |
| 5 | `[(5, 2)]` | `{0: 1, -1: 2, 1: 3}` | Pop `(4,0)`. HD 0 exists in map (val=1), skip insertion! |
| 6 | `[]` | `{0: 1, -1: 2, 1: 3, 2: 5}` | Pop `(5,2)`. Add `2:5` to map. Queue empty. |

**Result (sorted HD -1 to 2):** `[2, 1, 3, 5]`

---

## Edge Cases

- **Empty Tree:** Return `[]`.
- **Single Node:** Return `[root.val]`.
- **Skewed Tree (Left/Right):** Processes linearly, HDs are strictly decreasing or increasing.
- **Overlapping Horizontal Distances at same level:** BFS level order natural ordering handles left-to-right correctly.

---

## Mistakes

- Using DFS instead of BFS without keeping track of level height (DFS can overwrite a top node with a deeper node if not careful).
- Overwriting the HashMap key when a new node at the same HD is encountered (Top view requires *only the first* node at each HD).
- Sorting map keys explicitly leading to extra O(K log K) time instead of tracking `min_hd` and `max_hd`.
- **User Mistake:** No specific note provided.

---

## Complexity

Time: O(N) → Every node is visited once during BFS traversal.
Space: O(N) → Queue and Hash Map store at most N elements.

---

## Similar Problems

- [Bottom View of Binary Tree](https://www.geeksforgeeks.org/problems/bottom-view-of-binary-tree/1) - Medium
- [Vertical Order Traversal of a Binary Tree](https://leetcode.com/problems/vertical-order-traversal-of-a-binary-tree/) - Hard
- [Binary Tree Right Side View](https://leetcode.com/problems/binary-tree-right-side-view/) - Medium

---

## Tags and Properties

- #dsa #important #revisit
- #binary-tree #top-view #level-order-traversal
- [[Trees]] [[Breadth First Search]] [[HashMap]]
- **Revision Date:** 2026-09-08
- **Problem Link:** [GeeksforGeeks - Top View of Binary Tree](https://www.geeksforgeeks.org/problems/top-view-of-binary-tree/1)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-09-10)
- [ ] Day 7 Revision (2026-09-15)
- [ ] Day 15 Revision (2026-09-23)
- [ ] Day 30 Revision (2026-10-08)
