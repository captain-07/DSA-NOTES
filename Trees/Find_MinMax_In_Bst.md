---
created: 2026-09-11
revisions:
  - 2026-09-13
  - 2026-09-18
  - 2026-09-26
  - 2026-10-11
---

# Find Min/Max In Bst

---

## Metadata & Placement Tags

- **Folder:** Trees
- **Target Companies:** #Amazon #Microsoft #Google #Facebook #Adobe

- **Confidence Checklist:**
  - [ ] Low
  - [ ] Medium
  - [ ] High

- **Concepts:** #bst [[Binary Search Tree]], #tree [[Tree Traversal]], #recursion [[Recursion]]

## Pattern

Binary Search Tree Property (BST Inorder / Directional Traversal)

---
## Difficulty

Easy #easy

---

## ⚡ Key Idea (Core Insight)

In a Binary Search Tree (BST), all values in the left subtree are smaller than the root, and all values in the right subtree are larger. Thus, the **minimum value** is the leftmost node (traverse `left` until `None`), and the **maximum value** is the rightmost node (traverse `right` until `None`).

---

## ⚡ Quick Recall (VERY IMPORTANT)

- Min element = keep moving `left` until `node.left` is `None`.
- Max element = keep moving `right` until `node.right` is `None`.

---

## Approach

### Brute Force
- Perform any tree traversal (Inorder/Preorder/Postorder), store nodes in an array, and find min/max.
- Time: O(N) | Space: O(N)

### Optimal
- Use BST properties to iteratively move `left` for min and `right` for max without storing nodes.
- Time: O(H) where H is tree height | Space: O(1)

---

## Code (Python)

```python
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    def find_min(self, root: TreeNode) -> int:
        if not root:
            return -1  # Or handle empty tree appropriately

        current_node = root
        # Keep traversing left to find the smallest element
        while current_node.left:
            current_node = current_node.left

        return current_node.val

    def find_max(self, root: TreeNode) -> int:
        if not root:
            return -1  # Or handle empty tree appropriately

        current_node = root
        # Keep traversing right to find the largest element
        while current_node.right:
            current_node = current_node.right

        return current_node.val
```

---

## Dry Run (Smart Example)

Input BST: Root = `15`, Left = `10` (Left child of 10 is `-5`), Right = `20` (Right child of 20 is `30`)

**Finding Min:**

| Step | Variables | Explanation |
| :--- | :--- | :--- |
| 1 | `current_node = Node(15)` | Start at root `15`. `left` exists (`10`). Move left. |
| 2 | `current_node = Node(10)` | Node is `10`. `left` exists (`-5`). Move left. |
| 3 | `current_node = Node(-5)` | Node is `-5`. `left` is `None`. Stop loop. |
| 4 | `Return -5` | Return `current_node.val` which is `-5`. |

---

## Edge Cases

- **Empty Tree (`root == None`):** Return indicative value (e.g., `-1` or `None`).
- **Single Node Tree:** Root is both min and max.
- **Skewed Tree (Left-skewed):** Min is at deep left; Max is root.
- **Skewed Tree (Right-skewed):** Min is root; Max is at deep right.

---

## Mistakes

- User mistake: No specific note provided.
- Forgetting to handle the empty tree base case (`root is None`).
- Confusing normal Binary Tree search (O(N)) with BST search (O(H)).
- Using recursion unnecessarily, which takes O(H) auxiliary call stack space instead of O(1) iterative space.

---

## Complexity

- **Time:** O(H) → H is tree height (O(log N) for balanced BST, O(N) for skewed BST).
- **Space:** O(1) → Iterative traversal uses constant extra space.

---

## Similar Problems

- [Search in a Binary Search Tree](https://leetcode.com/problems/search-in-a-binary-search-tree/) - Easy
- [Insert into a Binary Search Tree](https://leetcode.com/problems/insert-into-a-binary-search-tree/) - Medium
- [Lowest Common Ancestor of a Binary Search Tree](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-search-tree/) - Medium

---

## Tags and Properties

- #dsa #important #revisit #bst #tree
- Concepts: [[Binary Search Tree]], [[Tree Traversal]]
- Revision Date: 2026-09-11
- **Problem Link:** [GeeksforGeeks - Minimum element in BST](https://www.geeksforgeeks.org/problems/minimum-element-in-bst/1)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-09-13)
- [ ] Day 7 Revision (2026-09-18)
- [ ] Day 15 Revision (2026-09-26)
- [ ] Day 30 Revision (2026-10-11)
