---
created: 2026-09-08
revisions:
  - 2026-09-10
  - 2026-09-15
  - 2026-09-23
  - 2026-10-08
---

# Bottom View Of Binary Tree

---

## Metadata & Placement Tags

- **Folder:** Trees
- **Target Companies:** #Amazon #Flipkart #Paytm #Walmart #MakeMyTrip
- **Confidence Checklist:**
  - [ ] Low
  - [ ] Medium
  - [ ] High

- **Concepts:**
  - #trees [[Binary Tree]], #bfs [[Breadth-First Search]], #hashmap [[HashMap]], #verticaltraversal [[Vertical Order Traversal]]

## Pattern

BFS (Level Order Traversal) + Horizontal Distance Mapping with Hash Table

---
## Difficulty

Medium #medium

---

## ⚡ Key Idea (Core Insight)

- Assign a Horizontal Distance (HD) to each node: root is `0`, left child is `hd - 1`, right child is `hd + 1`.
- Perform BFS (level-order traversal) so that nodes at deeper levels overwrite previous nodes at the same HD in a map.
- The map will end up containing the last visible node for each horizontal distance from left to right.

---

## ⚡ Quick Recall (VERY IMPORTANT)

- BFS + Map key `HD` to `Node value`. Deeper nodes overwrite earlier nodes at the same HD. Print values sorted by HD.

---

## Approach

### Brute Force
- Recursive DFS to store `(value, depth)` for each `HD`, updating map only if current depth `≥` stored depth.
- Time: O(N log N) or O(N²), Space: O(N).

### Optimal
- Use BFS with a Queue storing tuples of `(node, hd)`.
- Use a Map (or Hash Table) to map `hd -> node.data`.
- Overwrite map values as BFS progresses (ensures bottom-most/latest level node remains).
- Track minimum and maximum HD to extract values in sorted HD order without explicit sorting overhead.

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
    def bottomView(self, root: TreeNode) -> list[int]:
        if not root:
            return []

        # Hash map to store horizontal distance (HD) -> node value
        hd_map = {}

        # Queue for BFS storing tuples of (node, horizontal_distance)
        queue = deque([(root, 0)])

        # Keep track of min and max HD to avoid sorting keys at the end
        min_hd, max_hd = 0, 0

        while queue:
            curr_node, hd = queue.popleft()

            # Overwrite the value at horizontal distance 'hd'
            # Later (deeper) nodes automatically overwrite earlier ones
            hd_map[hd] = curr_node.val

            # Update boundaries of horizontal distance
            min_hd = min(min_hd, hd)
            max_hd = max(max_hd, hd)

            # Add left child with HD - 1
            if curr_node.left:
                queue.append((curr_node.left, hd - 1))

            # Add right child with HD + 1
            if curr_node.right:
                queue.append((curr_node.right, hd + 1))

        # Reconstruct result from leftmost HD to rightmost HD
        result = []
        for hd in range(min_hd, max_hd + 1):
            result.append(hd_map[hd])

        return result
```

---

## Dry Run (Smart Example)

Tree:
```text
        20
       /  \
      8    22
     / \     \
    5   3     25
       / \
      10  14
```

| Step | Variables | Explanation |
| :--- | :--- | :--- |
| **1** | `queue=[(20,0)]`, `hd_map={}` | Initialize root at `HD=0`. |
| **2** | `curr=(20,0)`, `hd_map={0:20}` | Pop 20, set `hd_map[0]=20`. Push left (8,-1) and right (22,1). |
| **3** | `curr=(8,-1)`, `hd_map={0:20, -1:8}` | Pop 8, set `hd_map[-1]=8`. Push (5,-2) and (3,0). |
| **4** | `curr=(22,1)`, `hd_map={..., 1:22}` | Pop 22, set `hd_map[1]=22`. Push (25,2). |
| **5** | `curr=(5,-2)`, `hd_map={..., -2:5}` | Pop 5, set `hd_map[-2]=5`. |
| **6** | `curr=(3,0)`, `hd_map={..., 0:3}` | Pop 3, **overwrites HD 0** with value `3`. Push (10,-1) & (14,1). |
| **7** | `curr=(25,2)`, `hd_map={..., 2:25}` | Pop 25, set `hd_map[2]=25`. |
| **8** | `curr=(10,-1)`, `hd_map={..., -1:10}` | Pop 10, **overwrites HD -1** with `10`. |
| **9** | `curr=(14,1)`, `hd_map={..., 1:14}` | Pop 14, **overwrites HD 1** with `14`. |
| **End**| Range `-2` to `2` | Result: `[5, 10, 3, 14, 25]` |

---

## Edge Cases

- **Empty Tree (`root = None`):** Return `[]`.
- **Single Node Tree:** Returns `[root.val]` at `HD = 0`.
- **Skewed Tree (Line/LinkedList structure):** Works correctly as each node receives a distinct HD.
- **Overlapping Bottom Nodes at Same HD & Level:** The rightmost node visited last at that level overwrites and stays.

---

## Mistakes

- Using DFS without tracking node depth (DFS might visit a shallower node after a deeper node at the same HD).
- Forgetting that BFS automatically processes level-by-level, making simple overwrite work correctly.
- Sorting `hd_map.keys()` unnecessarily; maintain `min_hd` and `max_hd` for O(N) linear iteration.
- **User mistake:** No specific note provided.

---

## Complexity

Time: O(N) → Every node is processed exactly once via BFS.
Space: O(N) → Queue and hash map store at most N elements.

---

## Similar Problems

- [Top View of Binary Tree](https://www.geeksforgeeks.org/problems/top-view-of-binary-tree/1) - Medium
- [Vertical Order Traversal of a Binary Tree](https://leetcode.com/problems/vertical-order-traversal-of-a-binary-tree/) - Hard
- [Binary Tree Right Side View](https://leetcode.com/problems/binary-tree-right-side-view/) - Medium

---

## Tags and Properties

- #dsa #important #revisit #trees #bfs #bottomview
- Concepts: [[Trees]], [[Breadth-First Search]], [[HashMap]]
- **Revision Date:** 2026-09-08
- **Problem Link:** [Bottom View of Binary Tree - GeeksforGeeks](https://www.geeksforgeeks.org/problems/bottom-view-of-binary-tree/1)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-09-10)
- [ ] Day 7 Revision (2026-09-15)
- [ ] Day 15 Revision (2026-09-23)
- [ ] Day 30 Revision (2026-10-08)
