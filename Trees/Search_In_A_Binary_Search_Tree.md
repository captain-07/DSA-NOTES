---
created: 2026-09-11
revisions:
  - 2026-09-13
  - 2026-09-18
  - 2026-09-26
  - 2026-10-11
---

# Search In A Binary Search Tree

---

## Metadata & Placement Tags

- **Folder:** Trees
- **Target Companies:** #Amazon #Google #Microsoft #Facebook #LeetCode
- **Confidence Checklist:**
  - [ ] Low
  - [ ] Medium
  - [ ] High

- **Concepts:**
  - #bst [[Binary Search Tree]], #trees [[Trees]], #binarysearch [[Binary Search]], #iteration [[Iteration]]

## Pattern

Binary Search Tree Invariant Traversal / Binary Search

---
## Difficulty

Easy #easy

---

## ⚡ Key Idea (Core Insight)

Leverage the BST property: for any node, all left subtree values are strictly smaller and all right subtree values are strictly larger. Compare target `val` with `root.val` to eliminate half the tree at each step.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Compare target with `curr.val`: go left if `val < curr.val`, go right if `val > curr.val`. Iterative is preferred over recursive to achieve $O(1)$ auxiliary space.

---

## Approach

### Brute Force
- Perform a full Tree Traversal (DFS/BFS) ignoring BST properties.
- Time Complexity: $O(N)$, Space Complexity: $O(N)$ due to stack/queue call overhead.

### Optimal 1: Recursive
- Standard recursive BST traversal going left or right depending on node value.
- Time Complexity: $O(H)$, Space Complexity: $O(H)$ recursion call stack.

### Optimal 2: Iterative (Recommended)
- Traverse using a `while root` loop updating `root = root.left` or `root = root.right`.
- Eliminates function call overhead and saves call stack memory.
- Time Complexity: $O(H)$, Space Complexity: $O(1)$.

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
    def searchBST(self, root: Optional[TreeNode], val: int) -> Optional[TreeNode]:
        curr = root

        # Traverse the BST iteratively until node is found or reach null
        while curr is not None:
            if curr.val == val:
                return curr  # Found target node
            elif val < curr.val:
                curr = curr.left  # Target is smaller, search left subtree
            else:
                curr = curr.right  # Target is larger, search right subtree

        return None  # Value does not exist in BST
```

---

## Dry Run (Smart Example)

Input BST: `root = [4, 2, 7, 1, 3]`, `val = 2`

| Step | Variables | Explanation |
| :--- | :--- | :--- |
| 1 | `curr = Node(4)` | `2 < 4`, move left to `curr.left` |
| 2 | `curr = Node(2)` | `2 == 2`, target matched |
| 3 | Return `Node(2)` | Search terminates successfully, return subtree rooted at 2 |

---

## Edge Cases

- **Empty Tree (`root = None`):** Loop condition fails immediately, returns `None`.
- **Target Not Present:** Loop runs until `curr` becomes `None`, returns `None`.
- **Single Node Tree:** Returns node if value matches, else returns `None`.
- **Skewed BST (Line Graph):** Worst-case depth traversal works correctly.

---

## Mistakes

- Using recursive approach unnecessarily, leading to $O(H)$ extra stack space.
- Iterative approach is better because it avoids recursion call stack overhead ($O(1)$ space).
- Forgetting that BST nodes strictly follow `left < root < right`.

---

## Complexity

Time: $O(H)$ where $H$ is tree height ($O(\log N)$ average/balanced, $O(N)$ worst-case skewed).
Space: $O(1)$ iterative uses constant extra memory.

---

## Similar Problems

- [Insert into a Binary Search Tree](https://leetcode.com/problems/insert-into-a-binary-search-tree/) - Medium
- [Delete Node in a BST](https://leetcode.com/problems/delete-node-in-a-bst/) - Medium
- [Validate Binary Search Tree](https://leetcode.com/problems/validate-binary-search-tree/) - Medium
- [Kth Smallest Element in a BST](https://leetcode.com/problems/kth-smallest-element-in-a-bst/) - Medium

---

## Tags and Properties

- #dsa #important #revisit
- #binarytree #bst #iteration #tree-search
- [[Binary Search Tree]], [[Trees]], [[Binary Search]]
- **Revision Date:** 2026-09-11
- **Problem Link:** [Search in a Binary Search Tree - LeetCode](https://leetcode.com/problems/search-in-a-binary-search-tree/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-09-13)
- [ ] Day 7 Revision (2026-09-18)
- [ ] Day 15 Revision (2026-09-26)
- [ ] Day 30 Revision (2026-10-11)
