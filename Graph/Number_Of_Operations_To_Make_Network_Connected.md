---
created: 2026-10-30
revisions:
  - 2026-11-01
  - 2026-11-06
  - 2026-11-14
  - 2026-11-29
---

# Number Of Operations To Make Network Connected

---

## Metadata & Placement Tags

- **Folder:** Graph
- **Target Companies:**
  - #Amazon #Microsoft #Google #Cisco
- **Confidence Checklist:**
  - [ ] Low
  - [ ] Medium
  - [ ] High
- **Concepts:**
  - #connectedcomponents [[Connected Components]], #disjointsetunion [[Disjoint Set Union]], #dfs [[Depth First Search]], #bfs [[Breadth First Search]]

## Pattern

Connected Components Counting (DSU or DFS/BFS)

---
## Difficulty

Medium
#medium

---
## ⚡ Key Idea (Core Insight)

To connect `n` computers, you strictly need at least `n - 1` cables. If `len(connections) < n - 1`, it's impossible (`-1`). Otherwise, the minimum operations required is simply `(number of connected components) - 1`.

---
## ⚡ Quick Recall (VERY IMPORTANT)

If total edges < n - 1 return -1; else return `count_connected_components - 1`.

---
## Approach

### Brute Force
- Try removing each edge and testing overall connectivity via repeated graph traversals.
- Time Complexity: O(E * (V + E))

### Optimal
1. Check if total connections are sufficient (`len(connections) >= n - 1`). If not, return `-1`.
2. Model the computers as vertices `0` to `n - 1`.
3. Count the number of disconnected components using standard DFS/BFS or Disjoint Set Union (DSU).
4. The answer is `components - 1`.

---
## Code (Python)

```python
class Solution:
    def find_parent(self, parent: list, node: int) -> int:
        # Find root representative with path compression
        if parent[node] != node:
            parent[node] = self.find_parent(parent, parent[node])
        return parent[node]

    def union_nodes(self, parent: list, rank: list, node_u: int, node_v: int) -> int:
        root_u = self.find_parent(parent, node_u)
        root_v = self.find_parent(parent, node_v)

        # If already connected, no component count reduction
        if root_u == root_v:
            return 0

        # Union by rank
        if rank[root_u] < rank[root_v]:
            parent[root_u] = root_v
        elif rank[root_u] > rank[root_v]:
            parent[root_v] = root_u
        else:
            parent[root_v] = root_u
            rank[root_u] += 1

        return 1

    def makeConnected(self, n: int, connections: list[list[int]]) -> int:
        # Minimum n - 1 edges are required to connect n vertices
        if len(connections) < n - 1:
            return -1

        parent = list(range(n))
        rank = [0] * n
        components = n

        for u, v in connections:
            # Each successful union reduces component count by 1
            merged = self.union_nodes(parent, rank, u, v)
            components -= merged

        return components - 1
```

---
## Dry Run (Smart Example)

Input: `n = 6`, `connections = [[0,1],[0,2],[0,3],[1,2],[1,3]]`

| Step | Connection | Action / State | Components Left |
| :--- | :--- | :--- | :--- |
| Initial | - | Check `len(connections) = 5 >= 5`. Valid. | `6` (`{0},{1},{2},{3},{4},{5}`) |
| 1 | `[0,1]` | Union `0` and `1`. | `5` (`{0,1},{2},{3},{4},{5}`) |
| 2 | `[0,2]` | Union `0` and `2`. | `4` (`{0,1,2},{3},{4},{5}`) |
| 3 | `[0,3]` | Union `0` and `3`. | `3` (`{0,1,2,3},{4},{5}`) |
| 4 | `[1,2]` | `find(1) == find(2) == 0`. Redundant edge. | `3` (no change) |
| 5 | `[1,3]` | `find(1) == find(3) == 0`. Redundant edge. | `3` (no change) |
| Result | - | Return `components - 1 = 3 - 1 = 2`. | `2` operations needed |

---
## Edge Cases

- `len(connections) < n - 1`: Return `-1` immediately (not enough cables).
- `connections` is empty and `n == 1`: Valid case, requires `0` operations.
- Graph already fully connected: Result is `0` operations.
- Dense redundant connections with many isolated nodes: Handled correctly by DSU component reduction.

---
## Mistakes

- User Mistake: No specific note provided.
- Forgetting the early exit condition `len(connections) < n - 1`.
- Overcomplicating by trying to explicitly track which redundant edge moves where; only the counts matter.

---
## Complexity

Time: O(V + E * α(V)) → Processing all edges with near-constant DSU path compression and rank.
Space: O(V) → Storing `parent` and `rank` arrays of size `n`.

---
## Similar Problems

- [Number of Provinces](https://leetcode.com/problems/number-of-provinces/) - Medium
- [Redundant Connection](https://leetcode.com/problems/redundant-connection/) - Medium
- [Graph Valid Tree](https://leetcode.com/problems/graph-valid-tree/) - Medium
- [Accounts Merge](https://leetcode.com/problems/accounts-merge/) - Medium

---
## Tags and Properties

- #dsa #important #revisit #graph #unionfind #dfs
- [[Graph]] [[Connected Components]] [[Disjoint Set Union]]
- **Problem Link:** [Number of Operations to Make Network Connected - LeetCode](https://leetcode.com/problems/number-of-operations-to-make-network-connected/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-11-01)
- [ ] Day 7 Revision (2026-11-06)
- [ ] Day 15 Revision (2026-11-14)
- [ ] Day 30 Revision (2026-11-29)
