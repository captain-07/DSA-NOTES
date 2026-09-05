---
created: 2026-09-05
revisions:
  - 2026-09-07
  - 2026-09-12
  - 2026-09-20
  - 2026-10-05
---

# Binary Tree Maximum Path Sum

---

## Metadata & Placement Tags

- **Folder:** Trees
- **Target Companies:** #Facebook #Amazon #Google #Microsoft #Apple #Bloomberg

- **Confidence Checklist:**
  - [ ] Low
  - [ ] Medium
  - [ ] High

- **Concepts:**
  - #trees [[Trees]], #dfs [[Depth-First Search]], #recursion [[Recursion]], #tree-dp [[Tree DP]]

---
## Pattern

DFS / Post-Order Traversal + Tree DP

---
## Difficulty

Hard #hard

---

## ⚡ Key Idea (Core Insight)

At each node, calculate the maximum path sum going through it (Node + Left Gain + Right Gain). Update the global maximum sum, but return only `Node + max(Left Gain, Right Gain)` to the parent since a path cannot split.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Prune negative subtrees using `max(0, gain)`. Post-order traversal updates global `max_sum` with both branches, returns max single branch to parent.

---

## Approach

### Brute Force
- Compute path sum for every possible pair of nodes by traversing all paths.
- Time: $O(N^2)$, Space: $O(H)$

### Optimal
- Use post-order DFS to compute maximum contribution from left and right children bottom-up.
- Clamp negative contributions from subtrees to `0` using `max(0, subtree_gain)` since negative sums reduce overall path value.
- Update global max path sum at current node using `node.val + left_gain + right_gain`.
- Return `node.val + max(left_gain, right_gain)` to caller.

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
    def maxPathSum(self, root: TreeNode) -> int:
        self.max_sum = float('-inf')
        self.get_max_gain(root)
        return self.max_sum

    def get_max_gain(self, node: TreeNode) -> int:
        if not node:
            return 0

        # Ignore subtrees with negative sums by clamping gain to 0
        left_gain = max(0, self.get_max_gain(node.left))
        right_gain = max(0, self.get_max_gain(node.right))

        # Max path sum passing through the current node as the highest point (root of path)
        current_path_sum = node.val + left_gain + right_gain
        self.max_sum = max(self.max_sum, current_path_sum)

        # Return maximum single-branch path sum to the parent
        return node.val + max(left_gain, right_gain)
```

---

## Dry Run (Smart Example)

Tree: `[-10, 9, 20, null, null, 15, 7]`

| Step | Node / Call | Variables / Returns | Explanation |
| :--- | :--- | :--- | :--- |
| 1 | Leaf `9` | `left=0, right=0` | Path sum through `9` is `9`. Update `max_sum = 9`. Returns `9`. |
| 2 | Leaf `15` | `left=0, right=0` | Path sum through `15` is `15`. Update `max_sum = 15`. Returns `15`. |
| 3 | Leaf `7` | `left=0, right=0` | Path sum through `7` is `7`. Update `max_sum = 15`. Returns `7`. |
| 4 | Node `20` | `left_gain=15, right_gain=7` | Path sum through `20` is `20+15+7=42`. Update `max_sum = 42`. Returns `20 + max(15,7) = 35`. |
| 5 | Root `-10` | `left_gain=9, right_gain=35` | Path sum through `-10` is `-10+9+35=34`. `max_sum` remains `42`. |

---

## Edge Cases

- **Single Node:** Tree with only one node (returns node value, handles negative node).
- **All Negative Values:** e.g., `[-3, -2, -1]` -> Output should be `-1` (clamping negative gains to `0` prevents selecting empty paths).
- **Skewed Tree:** Call stack depth equals tree height $O(N)$.
- **Negative Subtrees:** Subtree with net negative sum is ignored due to `max(0, gain)`.

---

## Mistakes

- **Taking negative left/right gain:** Taking a negative left or right will never increase the `max_sum`, so exclude negatives using `max(0, gain)`.
- **Returning split path to parent:** Returning `node.val + left_gain + right_gain` upward breaks path definition (a valid path cannot branch twice).
- **Initializing max_sum to 0:** Fails when all node values in tree are negative. Initialize to `float('-inf')`.

---

## Complexity

Time: $O(N)$ → Visits every node exactly once during DFS traversal.
Space: $O(H)$ → Recursion stack uses space proportional to tree height $H$ ($O(N)$ worst, $O(\log N)$ average).

---

## Similar Problems

- [Path Sum](https://leetcode.com/problems/path-sum/) - Easy
- [Path Sum II](https://leetcode.com/problems/path-sum-ii/) - Medium
- [Binary Tree Longest Consecutive Sequence](https://leetcode.com/problems/binary-tree-longest-consecutive-sequence/) - Medium
- [Diameter of Binary Tree](https://leetcode.com/problems/diameter-of-binary-tree/) - Easy

---

## Tags and Properties

- #dsa #important #revisit #trees #dfs #binary-tree #interview-prep
- [[Trees]], [[Depth-First Search]], [[Recursion]]
- **Revision Date:** 2026-09-05
- **Problem Link:** [Binary Tree Maximum Path Sum - LeetCode](https://leetcode.com/problems/binary-tree-maximum-path-sum/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-09-07)
- [ ] Day 7 Revision (2026-09-12)
- [ ] Day 15 Revision (2026-09-20)
- [ ] Day 30 Revision (2026-10-05)
