---
created: 2026-09-16
revisions:
  - 2026-09-18
  - 2026-09-23
  - 2026-10-01
  - 2026-10-16
---

# Kth Largest Element In A Bst

---

## Metadata & Placement Tags

- **Folder:** Trees
- **Target Companies:** #Amazon #Microsoft #Facebook #Google #Uber
- **Confidence Checklist:**
  - [ ] Low
  - [ ] Medium
  - [ ] High

- **Concepts:**
  - #bst [[Binary Search Tree]], #inorder [[Inorder Traversal]], #tree [[Tree]]

## Pattern

Reverse Inorder Traversal (Right -> Node -> Left)

---
## Difficulty

Medium
Tag: #medium

---

## ⚡ Key Idea (Core Insight)

- Standard Inorder Traversal (Left -> Node -> Right) visits a BST in **sorted ascending order**.
- **Reverse Inorder Traversal (Right -> Node -> Left)** visits the BST in **sorted descending order**.
- By keeping a count of visited nodes, the $k$-th visited node is guaranteed to be the $k$-th largest element.

---

## ⚡ Quick Recall (VERY IMPORTANT)

- Perform Reverse Inorder (Right $\rightarrow$ Root $\rightarrow$ Left). Decrement $k$ at each node; when $k == 0$, the current node is the answer.

---

## Approach

### Brute Force
- Perform a full Inorder Traversal to collect all node values in an array (sorted ascending). Return the element at index `len(arr) - k`.
- Time: $O(N)$, Space: $O(N)$

### Optimal
- Use Reverse Inorder Traversal iteratively or recursively.
- Track remaining $k$ count using a class variable. Stop early as soon as $k$ reaches $0$ to avoid traversing unnecessary nodes.
- Time: $O(H + k)$, Space: $O(H)$ recursion stack space (where $H$ is tree height).

---

## Code (Python)

```python
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    def kthLargest(self, root: TreeNode, k: int) -> int:
        self.count = k
        self.result = -1
        self._reverse_inorder(root)
        return self.result

    def _reverse_inorder(self, node: TreeNode) -> None:
        # Base case or early stopping condition
        if node is None or self.count == 0:
            return

        # 1. Traverse Right subtree first (larger elements)
        self._reverse_inorder(node.right)

        # 2. Process current node
        self.count -= 1
        if self.count == 0:
            self.result = node.val
            return

        # 3. Traverse Left subtree (smaller elements)
        self._reverse_inorder(node.left)
```

---

## Dry Run (Smart Example)

**Input BST:** `root = [5, 3, 6, 2, 4, null, null]`, `k = 3`
(Structure: 5 is root; left is 3 with children 2, 4; right is 6)

| Step | Current Node | `self.count` (Remaining $k$) | Explanation |
|---|---|---|---|
| 1 | `Node(6)` | 3 $\rightarrow$ 2 | Go fully right to `Node(6)`. Visit node `6`, decrement $k$ to 2. |
| 2 | `Node(5)` | 2 $\rightarrow$ 1 | Backtrack to `Node(5)`. Visit node `5`, decrement $k$ to 1. |
| 3 | `Node(4)` | 1 $\rightarrow$ 0 | Move to left subtree of 5, then right child `Node(4)`. Decrement $k$ to 0. Target found! |

**Result:** `4`

---

## Edge Cases

- **$k = 1$:** Returns the maximum element in the BST (rightmost node).
- **$k = N$ (Total Nodes):** Returns the minimum element in the BST (leftmost node).
- **Skewed Tree (Line graph):** Height $H = N$, stack depth becomes $O(N)$.
- **Single Node Tree:** Returns root value if $k = 1$.

---

## Mistakes

- Traversing Left-first instead of Right-first, requiring full traversal and array indexing.
- Forgetting early exit, leading to unnecessary operations after finding the answer.
- **User Mistake:** No specific note provided.

---

## Complexity

Time: $O(H + k)$ → Traverses rightmost path to highest element, then visits $k$ nodes.
Space: $O(H)$ → Auxiliary recursion stack space proportional to tree height $H$.

---

## Similar Problems

- [Kth Smallest Element in a BST](https://leetcode.com/problems/kth-smallest-element-in-a-bst/) - Medium
- [Validate Binary Search Tree](https://leetcode.com/problems/validate-binary-search-tree/) - Medium
- [Inorder Successor in BST](https://leetcode.com/problems/inorder-successor-in-bst/) - Medium

---

## Tags and Properties

  - #dsa #important #revisit #trees #bst
  - [[Binary Search Tree]], [[Inorder Traversal]]
  - **Last Revised:** 2026-09-16
  - **Problem Link:** [Kth Largest Element in a BST - GeeksforGeeks](https://www.geeksforgeeks.org/problems/kth-largest-element-in-bst/1)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-09-18)
- [ ] Day 7 Revision (2026-09-23)
- [ ] Day 15 Revision (2026-10-01)
- [ ] Day 30 Revision (2026-10-16)
