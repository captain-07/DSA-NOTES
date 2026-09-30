---
created: 2026-09-30
revisions:
  - 2026-10-02
  - 2026-10-07
  - 2026-10-15
  - 2026-10-30
---

# Number Of Provinces

---

## Metadata & Placement Tags

- **Folder:** Graph
- **Target Companies:** #Amazon #Microsoft #Google #Facebook #Bloomberg
- **Confidence Checklist:**
  - [ ] Low
  - [ ] Medium
  - [ ] High

- **Concepts:**
  - #graph [[Graph]], #dfs [[Depth First Search]], #bfs [[Breadth First Search]], #unionfind [[Disjoint Set Union]]

## Pattern

Graph Traversal (DFS / BFS) / Disjoint Set Union (DSU)

---
## Difficulty

Medium
Tag: #medium

---

## ⚡ Key Idea (Core Insight)

The problem asks for the number of connected components in an undirected graph given as an adjacency matrix. Traverse each unvisited node using DFS/BFS to explore its entire connected component and increment the province count by 1 for each new traversal source.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Find number of connected components: Iterate through nodes `0` to `n-1`, launch DFS/BFS if unvisited, and increment component counter.

---

## Approach

### Brute Force
- N/A (Graph traversal O(V^2) matrix scanning is inherently optimal for given input matrix).
- Time: O(V^2)

### Better (BFS Traversal)
- Use a queue to iteratively visit all reachable nodes from an unvisited starting node.
- Time: O(V^2), Space: O(V)

### Optimal 1: DFS (Depth-First Search)
1. Maintain a `visited` array of size `V`.
2. Iterate `i` from `0` to `V-1`.
3. If node `i` is not visited, increment `province_count` and start DFS from `i`.
4. In DFS, mark current node visited and recursively visit all unvisited neighbors `j` where `isConnected[i][j] == 1`.

### Optimal 2: Union-Find (Disjoint Set Union)
1. Initialize DSU with `V` components (each node is its own parent).
2. Iterate over upper triangle of matrix (`i` from `0` to `V-1`, `j` from `i+1` to `V-1`).
3. If `isConnected[i][j] == 1`, union sets containing `i` and `j`. If successful, reduce component count by 1.

---

## Code (Python)

### Approach 1: DFS

```python
class Solution:
    def findCircleNum(self, isConnected: list[list[int]]) -> int:
        num_cities = len(isConnected)
        visited = [False] * num_cities
        province_count = 0

        # Iterate over all cities
        for city in range(num_cities):
            # Start DFS if the city hasn't been visited yet
            if not visited[city]:
                province_count += 1
                self._dfs(city, isConnected, visited)

        return province_count

    def _dfs(self, current_city: int, isConnected: list[list[int]], visited: list[bool]) -> None:
        visited[current_city] = True

        # Check all neighboring cities
        for neighbor in range(len(isConnected)):
            # Visit connected and unvisited neighbors
            if isConnected[current_city][neighbor] == 1 and not visited[neighbor]:
                self._dfs(neighbor, isConnected, visited)
```

### Approach 2: Disjoint Set Union (DSU)

```python
class UnionFind:
    def __init__(self, size: int):
        self.parent = list(range(size))
        self.count = size

    def find(self, node: int) -> int:
        if self.parent[node] != node:
            # Path compression
            self.parent[node] = self.find(self.parent[node])
        return self.parent[node]

    def union(self, node1: int, node2: int) -> None:
        root1 = self.find(node1)
        root2 = self.find(node2)
        if root1 != root2:
            self.parent[root1] = root2
            self.count -= 1

class Solution:
    def findCircleNum(self, isConnected: list[list[int]]) -> int:
        num_cities = len(isConnected)
        uf = UnionFind(num_cities)

        # Traverse upper triangular matrix to find connections
        for row in range(num_cities):
            for col in range(row + 1, num_cities):
                if isConnected[row][col] == 1:
                    uf.union(row, col)

        return uf.count
```

---

## Dry Run (Smart Example)

Input: `isConnected = [[1,1,0],[1,1,0],[0,0,1]]` (3 cities)

| Step | Variables | Explanation |
| :--- | :--- | :--- |
| 1 | `city=0`, `visited=[F,F,F]`, `count=0` | `visited[0]` is False. Increments `count` to 1, calls `_dfs(0)`. |
| 2 | `_dfs(0)`, `visited=[T,F,F]` | Marks 0 visited. Neighbor 1 is connected (`matrix[0][1]==1`), calls `_dfs(1)`. |
| 3 | `_dfs(1)`, `visited=[T,T,F]` | Marks 1 visited. Neighbor 0 is visited. Neighbor 2 not connected. Returns back to outer loop. |
| 4 | `city=1`, `visited=[T,T,F]` | `visited[1]` is True. Skip. |
| 5 | `city=2`, `visited=[T,T,F]`, `count=1` | `visited[2]` is False. Increments `count` to 2, calls `_dfs(2)`. Marks 2 visited. |
| 6 | End of loop | Returns final `count = 2`. |

---

## Edge Cases

- **Single city (`n = 1`):** Matrix `[[1]]`, returns 1 province directly.
- **Disconnected graph:** Diagonal is 1s, rest 0s; returns `n` provinces.
- **Fully connected graph:** All matrix entries are 1; returns 1 province.

---

## Mistakes

- Forgetting that matrix represents undirected edges (`isConnected[i][j] == isConnected[j][i]`).
- Re-checking visited nodes in outer loop without checking `visited[city]` flag.
- Confusing adjacency matrix input with adjacency list.
- User Mistake: No specific note provided.

---

## Complexity

Time: O(V^2) → Must scan all `V * V` matrix elements to check connectivity.
Space: O(V) → Visited array of size `V` plus O(V) call stack for DFS.

---

## Similar Problems

- [Number of Connected Components in an Undirected Graph](https://leetcode.com/problems/number-of-connected-components-in-an-undirected-graph/) - Medium
- [Number of Islands](https://leetcode.com/problems/number-of-islands/) - Medium
- [Redundant Connection](https://leetcode.com/problems/redundant-connection/) - Medium

---

## Tags and Properties

- #dsa #important #revisit
- #graph #dfs #disjointset
- [[Graph]], [[Depth First Search]], [[Disjoint Set Union]]
- **Revision Date:** 2026-09-30
- **Problem Link:** [Number Of Provinces - LeetCode](https://leetcode.com/problems/number-of-provinces/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-10-02)
- [ ] Day 7 Revision (2026-10-07)
- [ ] Day 15 Revision (2026-10-15)
- [ ] Day 30 Revision (2026-10-30)
