---
created: 2026-09-04
revisions:
  - 2026-09-06
  - 2026-09-11
  - 2026-09-19
  - 2026-10-04
---

# Diameter Of Binary Tree

---

## Metadata & Placement Tags

- **Folder:** Trees
- **Target Companies:** #Amazon #Facebook #Google #Microsoft #Bloomberg #Apple

- **Confidence Checklist:**
  - [ ] Low
  - [ ] Medium
  - [ ] High

- **Concepts:**
  - #trees [[Trees]], #dfs [[Depth First Search]], #binarytree [[Binary Tree]], #recursion [[Recursion]]

## Pattern

DFS / Tree Depth Calculation (Bottom-Up Postorder Traversal)

---
## Difficulty

Easy
#easy

---

## ⚡ Key Idea (Core Insight)

The diameter at any node is the sum of the maximum depths of its left and right subtrees (`left_height + right_height`). We compute the height of every node recursively using postorder traversal while updating a global maximum diameter.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Diameter at node = `height(left) + height(right)`. Return `1 + max(height(left), height(right))` to parent.

---

## Approach

### Brute Force
- Calculate the height of left and right subtrees for every node separately using a standalone height function.
- Time: O(N²) | Space: O(H) where H is tree height.

### Optimal
- Use a single postorder DFS traversal to calculate heights bottom-up.
- At each node, compute `left_height` and `right_height`, update global maximum diameter (`left_height + right_height`), and return node's height `1 + max(left_height, right_height)`.
- Time: O(N) | Space: O(H).

---

## Code (Python)

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right

class Solution:
    def diameterOfBinaryTree(self, root: Optional[TreeNode]) -> int:
        self.max_diameter = 0
        self._calculate_height(root)
        return self.max_diameter

    def _calculate_height(self, node: Optional[TreeNode]) -> int:
        if not node:
            return 0

        # Bottom-up recursion: find height of left and right subtrees
        left_height = self._calculate_height(node.left)
        right_height = self._calculate_height(node.right)

        # Path passing through current node as root of subtree
        current_diameter = left_height + right_height

        # Update global maximum diameter found so far
        self.max_diameter = max(self.max_diameter, current_diameter)

        # Return height of subtree rooted at current node
        return 1 + max(left_height, right_height)
```

---

## Dry Run (Smart Example)

Tree: `[1, 2, 3, 4, 5]`
Structure: Node 1 has left 2, right 3. Node 2 has left 4, right 5.

| Step | Node | Variables | Explanation |
| :--- | :--- | :--- | :--- |
| 1 | `4` & `5` | `lh=0, rh=0` | Leaf nodes return height `1`. `max_diameter = max(0, 0+0) = 0`. |
| 2 | `2` | `lh=1, rh=1` | Subtrees 4 & 5 return 1. `max_diameter = max(0, 1+1) = 2`. Returns height `2`. |
| 3 | `3` | `lh=0, rh=0` | Leaf node returns height `1`. `max_diameter = max(2, 0+0) = 2`. |
| 4 | `1` | `lh=2, rh=1` | Subtree 2 returns 2, Subtree 3 returns 1. `max_diameter = max(2, 2+1) = 3`. |

---

## Edge Cases

- **Single Node Tree:** Returns `0` diameter as there are no edges.
- **Skewed Tree (Line graph):** Correctly traverses down single path, height equals diameter.
- **Empty Tree (`root = None`):** Returns `0`.
- **Diameter path does NOT pass through the root:** Handled automatically because `max_diameter` is updated at every internal node.

---

## Mistakes

- User mistake: No specific note provided.
- Forgetting that diameter is measured in **edges** (number of nodes - 1 along the longest path).
- Assuming the longest path must pass through the root node.
- Re-calculating height at each node creating an unnecessary O(N²) time complexity.

---

## Complexity

Time: O(N) → Visits each node exactly once.
Space: O(H) → Recursion call stack uses O(H) memory, where H is tree height (O(N) worst case, O(log N) balanced).

---

## Similar Problems

- [Balanced Binary Tree](https://leetcode.com/problems/balanced-binary-tree/) - Easy
- [Binary Tree Maximum Path Sum](https://leetcode.com/problems/binary-tree-maximum-path-sum/) - Hard
- [Longest Path With Different Adjacent Characters](https://leetcode.com/problems/longest-path-with-different-adjacent-characters/) - Hard

---

## Tags and Properties

- #dsa #important #revisit
- #trees [[Trees]], #dfs [[Depth First Search]]
- Last Revised: 2026-09-04
- **Problem Link:** [Diameter of Binary Tree - LeetCode](https://leetcode.com/problems/diameter-of-binary-tree/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-09-06)
- [ ] Day 7 Revision (2026-09-11)
- [ ] Day 15 Revision (2026-09-19)
- [ ] Day 30 Revision (2026-10-04)
