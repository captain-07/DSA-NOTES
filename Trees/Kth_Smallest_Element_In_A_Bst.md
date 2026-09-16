---
created: 2026-09-16
revisions:
  - 2026-09-18
  - 2026-09-23
  - 2026-10-01
  - 2026-10-16
---

# Kth Smallest Element In A Bst

---

## Metadata & Placement Tags

- **Folder:** Trees
- **Target Companies:** #Amazon #Google #Microsoft #Facebook #Uber #Oracle
- **Confidence Checklist:**
  - [ ] Low
  - [ ] Medium
  - [ ] High
- **Concepts:** #bst [[Binary Search Tree]], #inorder [[Inorder Traversal]], #tree [[Tree]]

---

## Pattern

Inorder Traversal (Tree Traversal)

---

## Difficulty

Medium
#medium

---

## ⚡ Key Idea (Core Insight)

An **inorder traversal** (Left $\rightarrow$ Node $\rightarrow$ Right) of a Binary Search Tree (BST) visits nodes in strictly **sorted ascending order**. Counting nodes during an inorder traversal allows us to stop as soon as we reach the $k$-th visited element.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Perform Inorder Traversal (Iterative with stack or Recursive); decrement $k$ at each node visited, and return the node value when $k = 0$.

---

## Approach

### Brute Force
- Perform a full tree traversal, store all elements in an array, sort or access the $(k-1)$-th index.
- **Time:** $O(N)$, **Space:** $O(N)$

### Better
- Perform full inorder traversal to collect sorted elements in a list, then return `list[k-1]`.
- **Time:** $O(N)$, **Space:** $O(N)$

### Optimal (Iterative Inorder Traversal)
1. Use an explicit stack to traverse tree iteratively (inorder).
2. Push all left children to stack until reaching `None`.
3. Pop from stack, decrement $k$.
4. If $k == 0$, return popped node's value.
5. Move to popped node's right child and repeat.

---

## Code (Python)

```python
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    def kthSmallest(self, root: TreeNode, k: int) -> int:
        stack = []
        current = root

        # Traverse tree iteratively using stack
        while current is not None or len(stack) > 0:
            # Go as deep left as possible
            while current is not None:
                stack.append(current)
                current = current.left

            # Process node
            current = stack.pop()
            k -= 1

            # If k reaches 0, we found the kth smallest element
            if k == 0:
                return current.val

            # Move to right subtree
            current = current.right

        return -1
```

---

## Dry Run (Smart Example)

**Input:** BST = `[5, 3, 6, 2, 4, None, None, 1]`, $k = 3$
Tree structure:
```text
       5
      / \
     3   6
    / \
   2   4
  /
 1
```

| Step | Stack Content | Current Node | $k$ Value | Explanation |
| :--- | :--- | :--- | :--- | :--- |
| 1 | `[5, 3, 2, 1]` | `1` | `3` | Pushed left path down to node `1`. Pop `1`. |
| 2 | `[5, 3, 2]` | `None` (after `1.right`) | `2` | $k \neq 0$. `1` has no right child. Pop `2`. |
| 3 | `[5, 3]` | `None` (after `2.right`) | `1` | $k \neq 0$. `2` has no right child. Pop `3`. |
| 4 | `[5]` | `3` | `0` | $k == 0$ reached! Return `3.val` ($3$). |

---

## Edge Cases

- **Single Node Tree ($N = 1, k = 1$):** Returns root value immediately.
- **Skewed Tree (Left/Right Skewed):** Stack correctly handles linear depth up to $O(N)$.
- **$k = 1$ (Smallest Element):** Finds minimum element (leftmost leaf node).
- **$k = N$ (Largest Element):** Visits all nodes before returning max value.

---

## Mistakes

- No specific note provided.
- Forgetting that inorder traversal of a BST gives sorted elements.
- Not stopping early when $k$ reaches 0 (processing the entire tree unnecessarily).
- Mismanaging the stack during iterative traversal leading to infinite loops.

---

## Complexity

- **Time:** $O(H + k)$ where $H$ is tree height $\rightarrow$ Stops as soon as $k$-th element is visited.
- **Space:** $O(H)$ $\rightarrow$ Memory used by stack for tree height ($O(\log N)$ average, $O(N)$ worst-case).

---

## Similar Problems

- [Kth Largest Element in a BST](https://leetcode.com/problems/kth-largest-element-in-a-bst/) - Medium
- [Validate Binary Search Tree](https://leetcode.com/problems/validate-binary-search-tree/) - Medium
- [Binary Search Tree Iterator](https://leetcode.com/problems/binary-search-tree-iterator/) - Medium
- [Second Minimum Node In a Binary Tree](https://leetcode.com/problems/second-minimum-node-in-a-binary-tree/) - Easy

---

## Tags and Properties

- #dsa #important #revisit #bst #inorder
- [[Binary Search Tree]] [[Inorder Traversal]] [[Tree]]
- **Last Revised:** 2026-09-16
- **Problem Link:** [LeetCode - Kth Smallest Element in a BST](https://leetcode.com/problems/kth-smallest-element-in-a-bst/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-09-18)
- [ ] Day 7 Revision (2026-09-23)
- [ ] Day 15 Revision (2026-10-01)
- [ ] Day 30 Revision (2026-10-16)
