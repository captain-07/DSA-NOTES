---
created: 2026-09-18
revisions:
  - 2026-09-20
  - 2026-09-25
  - 2026-10-03
  - 2026-10-18
---

# Predecessor And Successor In Bst

---

## Metadata & Placement Tags

- **Folder:** Trees
- **Target Companies:** #Amazon #Google #Microsoft #Facebook
- **Confidence Checklist:**
  - [ ] Low
  - [ ] Medium
  - [ ] High

- **Concepts:** #bst [[BST]], #trees [[Trees]], #inorder [[Inorder Traversal]]

## Pattern

Binary Search Tree Traversal / Binary Search Iteration

---
## Difficulty

Medium
#medium

---

## ⚡ Key Idea (Core Insight)

- Maintain `pre` and `succ` pointers while navigating down the BST using its ordering property.
- If `root.val < key`, the current node is a potential predecessor, so update `pre = root` and go right.
- If `root.val > key`, the current node is a potential successor, so update `succ = root` and go left.
- If `root.val == key`, predecessor is the rightmost node of the left subtree, and successor is the leftmost node of the right subtree.

---

## ⚡ Quick Recall (VERY IMPORTANT)

- Traverse tree once: update `pre` when going right, `succ` when going left. If key found, extract max from left child and min from right child.

---

## Approach

### Brute Force
- Store Inorder traversal in an array, then find `key` to get adjacent elements.
- Time: O(N), Space: O(N)

### Better
- Perform single pass Inorder traversal iteratively/recursively without array, keeping track of previous node.
- Time: O(N), Space: O(H) for recursion stack.

### Optimal
- Use BST properties to find predecessor and successor in a single pass iteratively.
- Time: O(H), Space: O(1)

---

## Code (Python)

```python
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    def findPredecessorSuccessor(self, root: TreeNode, key: int):
        predecessor = None
        successor = None
        current = root

        while current:
            if current.val == key:
                # Find maximum value in left subtree for predecessor
                if current.left:
                    temp = current.left
                    while temp.right:
                        temp = temp.right
                    predecessor = temp

                # Find minimum value in right subtree for successor
                if current.right:
                    temp = current.right
                    while temp.left:
                        temp = temp.left
                    successor = temp
                break

            elif current.val < key:
                # Potential predecessor found, move right
                predecessor = current
                current = current.right

            else:
                # Potential successor found, move left
                successor = current
                current = current.left

        return predecessor, successor
```

---

## Dry Run (Smart Example)

**Input BST:** `root = [5, 2, 7, 1, 4, 6, 9]`, `key = 3`

| Step | Variables | Explanation |
|---|---|---|
| 1 | `current = 5`, `key = 3` | `3 < 5` → Potential successor `succ = 5`, move to `current.left` (2). |
| 2 | `current = 2`, `key = 3` | `3 > 2` → Potential predecessor `pre = 2`, move to `current.right` (4). |
| 3 | `current = 4`, `key = 3` | `3 < 4` → Potential successor `succ = 4`, move to `current.left` (None). |
| 4 | `current = None` | Loop terminates. Return `pre = 2`, `succ = 4`. |

---

## Edge Cases

- **Key not present in BST:** Handled naturally by loop termination logic returning current `pre` and `succ`.
- **Key is smallest node:** Predecessor remains `None`.
- **Key is largest node:** Successor remains `None`.
- **Empty tree (`root = None`):** Returns `(None, None)`.

---

## Mistakes

- Using a two-pass optimal method finding successor and predecessor separately instead of doing it in a single pass traversal.
- Forgetting to check if left/right child exists when `current.val == key` before traversing.
- Assuming the key is always present in the tree.

---

## Complexity

Time: O(H) where H is the height of the BST (O(log N) for balanced, O(N) for skewed).
Space: O(1) auxiliary space using iterative traversal.

---

## Similar Problems

- [Inorder Successor in BST](https://leetcode.com/problems/inorder-successor-in-bst/) - Medium
- [Search in a Binary Search Tree](https://leetcode.com/problems/search-in-a-binary-search-tree/) - Easy
- [Insert into a Binary Search Tree](https://leetcode.com/problems/insert-into-a-binary-search-tree/) - Medium

---

## Tags and Properties

- #dsa #important #revisit
- #bst [[Binary Search Tree]], #inorder [[Inorder Traversal]]
- **Last Revised:** 2026-09-18
- **Problem Link:** [Predecessor and Successor - GeeksforGeeks](https://www.geeksforgeeks.org/problems/predecessor-and-successor/1)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-09-20)
- [ ] Day 7 Revision (2026-09-25)
- [ ] Day 15 Revision (2026-10-03)
- [ ] Day 30 Revision (2026-10-18)
