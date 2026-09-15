---
created: 2026-09-15
revisions:
  - 2026-09-17
  - 2026-09-22
  - 2026-09-30
  - 2026-10-15
---

# Insert Into A Binary Search Tree

---

## Metadata & Placement Tags

- **Folder:** Trees
- **Target Companies:** #Amazon #Microsoft #Google #Facebook #LeetCode
- **Confidence Checklist:**
  - [ ] Low
  - [ ] Medium
  - [ ] High

- **Concepts:**
  - #binarysearchtree [[Binary Search Tree]], #trees [[Trees]], #recursion [[Recursion]], #iteration [[Iteration]]

---

## Pattern

Binary Search Tree Traversal + Leaf Node Insertion

---

## Difficulty

Medium
#medium

---

## ⚡ Key Idea (Core Insight)

- Leverage the BST property: values smaller than the current node go to the left subtree, and values greater go to the right subtree.
- Traverse down to find a `None` spot (null position) where the node naturally belongs, create the new node there, and connect it to its parent.

---

## ⚡ Quick Recall (VERY IMPORTANT)

- Return the newly created node when reaching a `None` pointer during recursion, or attach it directly to the parent when `curr.left` / `curr.right` is `None` during iteration.

---

## Approach

### Brute Force
- Store all node values via in-order traversal into an array, insert the new value, sort the array, and rebuild a balanced BST.
- Time Complexity: O(N log N), Space Complexity: O(N).

### Better
- N/A (Standard traversal is already direct and optimal).

### Optimal

#### Method 1: Recursive Approach
1. Base case: If `root` is `None`, return `TreeNode(val)`.
2. If `val < root.val`, recursively insert into `root.left`: `root.left = self.insertIntoBST(root.left, val)`.
3. If `val > root.val`, recursively insert into `root.right`: `root.right = self.insertIntoBST(root.right, val)`.
4. Return `root`.

#### Method 2: Iterative Approach
1. Handle empty tree edge case (`root is None`).
2. Traverse the tree using a pointer `curr`.
3. If `val > curr.val`, check if `curr.right` is empty. If yes, insert and break; else move `curr = curr.right`.
4. If `val < curr.val`, check if `curr.left` is empty. If yes, insert and break; else move `curr = curr.left`.
5. Return original `root`.

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
    def insertIntoBST(self, root: TreeNode, val: int) -> TreeNode:
        # Base case: if tree or subtree is empty, return a new node
        if not root:
            return TreeNode(val)

        # Navigate left or right depending on the value comparison
        if val < root.val:
            root.left = self.insertIntoBST(root.left, val)
        else:
            root.right = self.insertIntoBST(root.right, val)

        return root

    def insertIntoBST_iterative(self, root: TreeNode, val: int) -> TreeNode:
        if not root:
            return TreeNode(val)

        current_node = root

        while True:
            # If target value is greater, go to the right subtree
            if val > current_node.val:
                if not current_node.right:
                    current_node.right = TreeNode(val)
                    break
                current_node = current_node.right
            # If target value is smaller, go to the left subtree
            else:
                if not current_node.left:
                    current_node.left = TreeNode(val)
                    break
                current_node = current_node.left

        return root
```

---

## Dry Run (Smart Example)

**Input:** `root = [4, 2, 7, 1, 3]`, `val = 5`

| Step | Current Node (`curr.val`) | Decision / Action | Resulting Tree Structure |
| :--- | :--- | :--- | :--- |
| 1 | `4` | `5 > 4` → Move to `curr.right` (`7`) | Traversal continues to node `7` |
| 2 | `7` | `5 < 7` → Move to `curr.left` (`None`) | `curr.left` is `None` |
| 3 | `None` (Recursive Base Case) | Create `TreeNode(5)` and return | Node `5` returned to parent `7` |
| 4 | `7` | Set `7.left = TreeNode(5)` | Node `5` is linked as left child of `7` |

---

## Edge Cases

- **Empty Tree (`root = None`):** Create and return `TreeNode(val)` as root directly.
- **Single Node Tree:** Correctly attaches as left or right child of root.
- **Unbalanced/Skewed BST:** Traverses down line length without failing.

---

## Mistakes

- **User Mistake:** Pre-checking left and right children prematurely and performing inline insertion logic incorrectly instead of letting recursion handle returning the new subtree node at `None`.
- Forgetting to re-assign returned node pointers: `root.left = insertIntoBST(...)`.
- Forgetting to handle the initial `root == None` condition.

---

## Complexity

- **Time:** O(H) → where H is height of BST (O(log N) for balanced BST, O(N) for skewed tree).
- **Space:** O(H) → recursion stack space (O(1) auxiliary space if using iterative approach).

---

## Similar Problems

- [Search in a Binary Search Tree](https://leetcode.com/problems/search-in-a-binary-search-tree/) - Easy
- [Delete Node in a BST](https://leetcode.com/problems/delete-node-in-a-bst/) - Medium
- [Kth Smallest Element in a BST](https://leetcode.com/problems/kth-smallest-element-in-a-bst/) - Medium

---

## Tags and Properties

- #dsa #important #revisit
- #bst #insertion #binarytree
- [[Binary Search Tree]], [[Trees]], [[Recursion]]
- **Revision Date:** 2026-09-15
- **Problem Link:** [Insert into a Binary Search Tree - LeetCode](https://leetcode.com/problems/insert-into-a-binary-search-tree/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-09-17)
- [ ] Day 7 Revision (2026-09-22)
- [ ] Day 15 Revision (2026-09-30)
- [ ] Day 30 Revision (2026-10-15)
