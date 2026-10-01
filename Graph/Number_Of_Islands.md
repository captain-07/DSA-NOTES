---
created: 2026-10-01
revisions:
  - 2026-10-03
  - 2026-10-08
  - 2026-10-16
  - 2026-10-31
---

# Number Of Islands

---

## Metadata & Placement Tags

- **Folder:** Graph
- **Target Companies:** #Amazon #Google #Microsoft #Meta #Bloomberg #Uber
- **Confidence Checklist:**
  - [ ] Low
  - [ ] Medium
  - [ ] High

- **Concepts:** #graph [[Graph]], #bfs [[Breadth-First Search]], #dfs [[Depth-First Search]], #unionfind [[Union Find]]

## Pattern

Grid Traversal + Connected Components (DFS / BFS)

---
## Difficulty

Medium
#medium

---

## ⚡ Key Idea (Core Insight)

Iterate through every cell in the grid. When an unvisited land cell (`'1'`) is found, increment the island counter and trigger a traversal (DFS/BFS) to sink/mark all connected land cells as visited (`'0'`).

---

## ⚡ Quick Recall (VERY IMPORTANT)

Traverse grid -> hit `'1'` -> increment count -> sink all connected land (`'1'` -> `'0'`) using DFS/BFS.

---

## Approach

### Brute Force
- Treat each land cell as a potential unique island and check all path combinations without marking visited cells.
- Time Complexity: O(4^(M*N)) (exponential due to infinite/redundant loops)

### Better
- Maintain a separate 2D boolean array `visited[M][N]` to track visited cells during DFS/BFS.
- Time Complexity: O(M * N), Space Complexity: O(M * N) extra space.

### Optimal
- Modify the input grid in-place by changing visited `'1'`s to `'0'`s ("sinking" the island) during traversal, eliminating the need for an explicit `visited` array.
- Step-by-step:
  1. Iterate over every cell `(r, c)` in the `M x N` grid.
  2. If `grid[r][c] == '1'`, increment `island_count` and start DFS/BFS from `(r, c)`.
  3. In DFS/BFS helper, turn current `'1'` into `'0'` and recursively/iteratively visit valid adjacent 4-directional neighbors.

---

## Code (Python)

```python
class Solution:
    def numIslands(self, grid: list[list[str]]) -> int:
        if not grid or not grid[0]:
            return 0

        rows = len(grid)
        cols = len(grid[0])
        island_count = 0

        # Iterate over every cell in the 2D grid
        for row in range(rows):
            for col in range(cols):
                # When land is found, it represents a new island
                if grid[row][col] == '1':
                    island_count += 1
                    # Sink the entire island using DFS
                    self._dfs(grid, row, col)

        return island_count

    def _dfs(self, grid: list[list[str]], row: int, col: int) -> None:
        rows = len(grid)
        cols = len(grid[0])

        # Base cases: out of bounds or water cell ('0')
        if row < 0 or row >= rows or col < 0 or col >= cols or grid[row][col] == '0':
            return

        # Sink the current land cell to mark it as visited
        grid[row][col] = '0'

        # Traverse 4-directionally (up, down, left, right)
        self._dfs(grid, row - 1, col)  # Up
        self._dfs(grid, row + 1, col)  # Down
        self._dfs(grid, row, col - 1)  # Left
        self._dfs(grid, row, col + 1)  # Right
```

---

## Dry Run (Smart Example)

Input:
`grid = [["1","1","0"],["1","0","0"],["0","0","1"]]`

| Step | Variables | Explanation |
| :--- | :--- | :--- |
| 1 | `row=0, col=0`, `island_count=1` | Found `'1'`. Increment count. Start DFS at `(0,0)`. |
| 2 | DFS sinks `(0,0)`, `(0,1)`, `(1,0)` | Sinks all connected land cells of 1st island to `'0'`. |
| 3 | `row=0..2`, `col=0..1` | Scans cells; all are now `'0'`. Skip. |
| 4 | `row=2, col=2`, `island_count=2` | Found `'1'`. Increment count. DFS sinks `(2,2)`. Returns `2`. |

---

## Edge Cases

- **Empty grid (`grid = []` or `grid = [[]]`)**: Return 0 immediately.
- **All water (`grid` full of `'0'`)**: Returns 0; no DFS triggered.
- **All land (`grid` full of `'1'`)**: Returns 1; single DFS sinks entire grid.
- **1x1 Grid**: Correctly returns 1 for `[["1"]]` and 0 for `[["0"]]`.

---

## Mistakes

- Forgetting boundary check conditions in DFS (`row < 0`, `col >= cols`, etc.).
- Not updating the cell to `'0'` *before* recursion, causing infinite stack overflow loops.
- User mistake: No specific note provided.

---

## Complexity

Time: O(M * N) → Every cell in the M x N grid is visited at most a constant number of times.
Space: O(M * N) → In the worst case (all land), call stack depth can grow up to O(M * N).

---

## Similar Problems

- [Max Area of Island](https://leetcode.com/problems/max-area-of-island/) - Medium
- [Number of Closed Islands](https://leetcode.com/problems/number-of-closed-islands/) - Medium
- [Surrounded Regions](https://leetcode.com/problems/surrounded-regions/) - Medium
- [Number of Enclaves](https://leetcode.com/problems/number-of-enclaves/) - Medium

---

## Tags and Properties

- #dsa #important #revisit
- #grid #graph-traversal #dfs
- [[Graph]], [[Breadth-First Search]], [[Depth-First Search]]
- **Last Revised:** 2026-10-01
- **Problem Link:** [Number of Islands - LeetCode](https://leetcode.com/problems/number-of-islands/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-10-03)
- [ ] Day 7 Revision (2026-10-08)
- [ ] Day 15 Revision (2026-10-16)
- [ ] Day 30 Revision (2026-10-31)
