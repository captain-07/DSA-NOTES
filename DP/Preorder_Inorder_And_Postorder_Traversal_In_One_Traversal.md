---
created: 2026-09-02
revisions:
  - 2026-09-04
  - 2026-09-09
  - 2026-09-17
  - 2026-10-02
---

# Preorder, Inorder, And Postorder Traversal In One Traversal

---

## Metadata & Placement Tags

- **Target Companies:** #Amazon #Microsoft #Google #TCS #Accenture
- **Confidence Checklist:**
  - [ ] Low
  - [ ] Medium
  - [ ] High
- **Concepts:** #binarytree [[Binary Tree]], #stack [[Stack]], #tree-traversal [[Tree Traversal]]

## Pattern

Stack Simulation + State Tracking

---
## Difficulty

Medium
#medium

---

## ⚡ Key Idea (Core Insight)

Use a single stack storing tuples of `(node, state)`.
- State `1`: Record in **Preorder**, increment state to `2`, push left child if present.
- State `2`: Record in **Inorder**, increment state to `3`, push right child if present.
- State `3`: Record in **Postorder**, pop from stack.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Stack element = `[node, state]`. State 1 → Pre & push left; State 2 → In & push right; State 3 → Post & pop.

---

## Approach

### Brute Force
- Perform three separate recursive/iterative traversals one after another.
- Time: $O(3N)$, Space: $O(N)$ stack space.

### Optimal
- Maintain a single stack storing `(node, state)` pairs initialized with `(root, 1)`.
- Process top element based on its state count (1, 2, or 3) to build all 3 traversal lists simultaneously in a single pass.
- Time: $O(N)$, Space: $O(N)$.

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
    def allTraversals(self, root: TreeNode) -> list[list[int]]:
        pre, ino, post = [], [], []
        if not root:
            return [pre, ino, post]

        # Stack elements: [node, state]
        stack = [[root, 1]]

        while stack:
            it = stack[-1]

            # State 1: Preorder -> Move to left
            if it[1] == 1:
                pre.append(it[0].val)
                it[1] += 1
                if it[0].left:
                    stack.append([it[0].left, 1])

            # State 2: Inorder -> Move to right
            elif it[1] == 2:
                ino.append(it[0].val)
                it[1] += 1
                if it[0].right:
                    stack.append([it[0].right, 1])

            # State 3: Postorder -> Pop node
            else:
                post.append(it[0].val)
                stack.pop()

        return [pre, ino, post]
```

---

## Dry Run (Smart Example)

Tree: `1 -> left: 2, right: 3`

| Step | Stack Top `(Node, State)` | Action & Explanation |
| :--- | :--- | :--- |
| 1 | `(1, 1)` | Preorder append `1`, state becomes `2`, push `(2, 1)`. |
| 2 | `(2, 1)` | Preorder append `2`, state becomes `2`, no children. Next step state `2` & `3` visit `2` for In/Post, pop `2`. |
| 3 | `(1, 2)` | Inorder append `1`, state becomes `3`, push `(3, 1)`. |
| 4 | `(3, 1)` | Preorder append `3`, processed for In/Post, popped. Finally `(1, 3)` postorder append `1` and popped. |

---

## Edge Cases

- **Empty Tree (`root = None`):** Handled gracefully by returning three empty lists `[[], [], []]`.
- **Single Node Tree:** Correctly processes Pre, In, and Post for the lone root node.
- **Skewed Tree (Left/Right):** Properly maintains state progression without missing recursive boundaries.

---

## Mistakes

- User mistake: No specific note provided.
- Forgetting to increment the state counter before pushing the child to the stack.
- Modifying node pointers instead of state counters during iterative processing.

---

## Complexity

Time: $O(N)$ → Every node is processed exactly 3 times (once per state).
Space: $O(N)$ → Stack holds at most $O(H)$ height nodes ($O(N)$ worst case).

---

## Similar Problems

- [Binary Tree Preorder Traversal](https://leetcode.com/problems/binary-tree-preorder-traversal/) - Easy
- [Binary Tree Inorder Traversal](https://leetcode.com/problems/binary-tree-inorder-traversal/) - Easy
- [Binary Tree Postorder Traversal](https://leetcode.com/problems/binary-tree-postorder-traversal/) - Easy

---

## Tags and Properties

- #dsa #important #revisit
- #tree #binarytree #stack #traversal
- [[Binary Tree]] [[Stack]] [[Tree Traversal]]
- **Revision Date:** 2026-09-02
- **Problem Link:** [GeeksforGeeks - Tree Traversals](https://www.geeksforgeeks.org/problems/tree-traversals/1)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-09-04)
- [ ] Day 7 Revision (2026-09-09)
- [ ] Day 15 Revision (2026-09-17)
- [ ] Day 30 Revision (2026-10-02)
