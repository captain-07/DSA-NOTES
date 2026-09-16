---
created: 2026-09-16
revisions:
  - 2026-09-18
  - 2026-09-23
  - 2026-10-01
  - 2026-10-16
---

# Delete Node In A Bst

---

## Metadata & Placement Tags

- **Folder:** Trees
- **Target Companies:** #Amazon #Microsoft #Google #Facebook #Uber
- **Confidence Checklist:**
  - [ ] Low
  - [ ] Medium
  - [ ] High

- **Concepts:** #bst [[Binary Search Tree]], #recursion [[Recursion]], #tree [[Trees]]

---

## Pattern

Binary Search Tree Traversal + Inorder Successor / Predecessor Substitution

---

## Difficulty

Medium #medium

---

## ⚡ Key Idea (Core Insight)

Locate the node using BST properties (`val < key` go right, `val > key` go left). Once found:
- If 0 or 1 child: Return non-null child (or `None`).
- If 2 children: Replace node value with min value from right subtree (inorder successor) and recursively delete that min node from the right subtree.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Search key in BST -> Node found -> Node with 2 children? Replace value with min of right subtree and delete successor. Otherwise return child node.

---

## Approach

### Brute Force
- Convert BST to array via inorder traversal, remove element, rebuild BST from array.
- Time: O(N), Space: O(N)

### Optimal
- Navigate to target node using BST search property.
- Handle target node deletion in-place recursively without breaking BST invariant.
- Time: O(H) where H is tree height, Space: O(H) call stack.

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
    def find_min(self, node: TreeNode) -> TreeNode:
        # Helper method to find the leftmost node (inorder successor)
        current = node
        while current.left:
            current = current.left
        return current

    def deleteNode(self, root: Optional[TreeNode], key: int) -> Optional[TreeNode]:
        if not root:
            return None

        # Search for key in left or right subtrees
        if key < root.val:
            root.left = self.deleteNode(root.left, key)
        elif key > root.val:
            root.right = self.deleteNode(root.right, key)
        else:
            # Case 1 & 2: Node has 0 or 1 child
            if not root.left:
                return root.right
            elif not root.right:
                return root.left

            # Case 3: Node has 2 children
            # Find inorder successor (smallest node in right subtree)
            successor = self.find_min(root.right)
            root.val = successor.val
            # Delete the inorder successor node
            root.right = self.deleteNode(root.right, successor.val)

        return root
```

---

## Dry Run (Smart Example)

Input Tree: `root = [5,3,6,2,4,null,7]`, `key = 3`

| Step | Variables | Explanation |
| :--- | :--- | :--- |
| 1 | `root.val = 5`, `key = 3` | `3 < 5`, recurse on `root.left` (node 3). |
| 2 | `root.val = 3`, `key = 3` | Key found! Node 3 has 2 children (2 and 4). |
| 3 | `successor.val = 4` | Min node in right subtree (`root.right=4`) is 4. Set `root.val = 4`. |
| 4 | `root.val = 4`, `key = 4` | Recurse `deleteNode(node 4, key=4)`. Node 4 has no children, returns `None`. |
| 5 | Return tree | Node 3 replaced by 4, original node 4 deleted. |

---

## Edge Cases

- `root` is `None`: Return `None`.
- `key` not present in BST: Return original tree unchanged.
- Target node is a leaf (no children): Directly remove node (return `None`).
- Target node has only left or right child: Replace target with its existing child.
- Target node is root of tree: Correctly updates root reference.

---

## Mistakes

- # Definition for a binary tree node.
- Forgetting to assign return value of recursive calls back to `root.left` / `root.right`.
- Replacing node with inorder successor value but failing to delete the duplicate successor node from right subtree.
- Attempting pointer manipulation instead of simple value substitution for 2-children case.

---

## Complexity

Time: O(H) → Height of tree (O(log N) balanced, O(N) worst-case skewed tree)
Space: O(H) → Call stack memory proportional to tree height

---

## Similar Problems

- [Insert into a Binary Search Tree](https://leetcode.com/problems/insert-into-a-binary-search-tree/) - Medium
- [Search in a Binary Search Tree](https://leetcode.com/problems/search-in-a-binary-search-tree/) - Easy
- [Inorder Successor in BST](https://leetcode.com/problems/inorder-successor-in-bst/) - Medium

---

## Tags and Properties

- #dsa #important #revisit #bst #trees
- [[Binary Search Tree]], [[Tree Traversal]], [[Recursion]]
- **Revision Date:** 2026-09-16
- **Problem Link:** [Delete Node in a BST - LeetCode](https://leetcode.com/problems/delete-node-in-a-bst/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-09-18)
- [ ] Day 7 Revision (2026-09-23)
- [ ] Day 15 Revision (2026-10-01)
- [ ] Day 30 Revision (2026-10-16)
