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
- **Target Companies:** #Amazon #Microsoft #Google #Meta #Adobe
- **Confidence Checklist:**
  - [ ] Low
  - [ ] Medium
  - [x] High

- **Concepts:**
  - #bst [[Binary Search Tree]], #trees [[Tree Search]], #iteration [[Iterative Search]]

## Pattern

Binary Search Tree Traversal / Binary Search Logic

---
## Difficulty

Easy / #easy

---

## ⚡ Key Idea (Core Insight)

- Leverage BST property: values in left subtree are smaller, values in right subtree are larger.
- Compare target with current node value: go left if target is smaller, go right if target is larger.

---

## ⚡ Quick Recall (VERY IMPORTANT)

- Treat BST search like binary search on an array: navigate left or right without exploring both subtrees.

---

## Approach

### Brute Force
- Traverse entire tree (e.g., DFS/BFS ignoring BST property) until target is found.
- Time: O(N), Space: O(N) stack/queue space.

### Optimal
1. Start at `root`.
2. While `node` is not `None` and `node.val != val`:
   - Move to `node.left` if `val < node.val`, else move to `node.right`.
3. Return `node`.

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
    def searchBST(self, root: TreeNode, val: int) -> TreeNode:
        current_node = root

        # Traverse the BST iteratively using BST property
        while current_node is not None and current_node.val != val:
            if val < current_node.val:
                current_node = current_node.left  # Search left subtree
            else:
                current_node = current_node.right  # Search right subtree

        return current_node
```

---

## Dry Run (Smart Example)

Input: `root = [4,2,7,1,3]`, `val = 2`

| Step | Variables | Explanation |
|---|---|---|
| 1 | `current_node.val = 4` | Target `2 < 4`, move left to `node 2`. |
| 2 | `current_node.val = 2` | Target `2 == 2`, loop condition breaks. |
| 3 | `current_node.val = 2` | Returns subtree rooted at node `2`. |

---

## Edge Cases

- `root` is `None`: Immediately returns `None`.
- Target value not in tree: Traverses until `current_node` becomes `None` and returns `None`.
- Single node tree: Correctly checks single node and returns result.

---

## Mistakes

- Using recursive approach unnecessarily: Iterative approach is better as it uses O(1) auxiliary space instead of O(H) recursion stack space.
- Searching both left and right subtrees like a normal binary tree instead of taking advantage of BST ordering.

---

## Complexity

Time: O(H) where H is tree height → O(log N) for balanced BST, O(N) for skewed tree.
Space: O(1) → Iterative approach uses constant auxiliary space.

---

## Similar Problems

- [Insert into a Binary Search Tree](https://leetcode.com/problems/insert-into-a-binary-search-tree/) - Medium
- [Delete Node in a BST](https://leetcode.com/problems/delete-node-in-a-bst/) - Medium
- [Search in Rotated Sorted Array](https://leetcode.com/problems/search-in-rotated-sorted-array/) - Medium

---

## Tags and Properties

  - #dsa #important #revisit
  - #bst #trees #binarysearch
  - obsidian links: [[Binary Search Tree]], [[Tree Traversal]]
  - Revision Date: 2026-09-11
  - **Problem Link:** [Search in a Binary Search Tree - LeetCode](https://leetcode.com/problems/search-in-a-binary-search-tree/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-09-13)
- [ ] Day 7 Revision (2026-09-18)
- [ ] Day 15 Revision (2026-09-26)
- [ ] Day 30 Revision (2026-10-11)
