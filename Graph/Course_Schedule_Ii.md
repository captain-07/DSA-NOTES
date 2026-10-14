---
created: 2026-10-14
revisions:
  - 2026-10-16
  - 2026-10-21
  - 2026-10-29
  - 2026-11-13
---

# Course Schedule Ii

---

## Metadata & Placement Tags

- **Folder:** Graph
- **Target Companies:** #Amazon #Google #Microsoft #Meta #Uber
- **Confidence Checklist:**
  - [ ] Low
  - [ ] Medium
  - [x] High
- **Concepts:** #topologicalsort [[Topological Sort]], #kahn [[Kahn's Algorithm]], #dfs [[Depth-First Search]], #dag [[Directed Acyclic Graph]]

## Pattern

Topological Sort (Kahn's BFS / In-degree Array) or DFS Cycle Detection

---
## Difficulty

Medium
#medium

---

## ⚡ Key Idea (Core Insight)

Model prerequisites as a Directed Acyclic Graph (DAG) with directed edges `prereq -> course`. A valid order is a **topological sort**; if the graph contains a cycle, no valid order exists.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Compute in-degrees for all nodes, queue up nodes with `in_degree == 0`, peel them layer by layer while decrementing neighbors' in-degrees, and append to the result list.

---

## Approach

### Brute Force
- Generate all `numCourses!` permutations and verify whether all prerequisite constraints hold.
- Time Complexity: $O(V! \times (V + E))$

### Better
- **DFS with 3-state coloring** (Unvisited=0, Visiting=1, Visited=2) to detect cycles and post-order reverse to construct topological order.
- Time Complexity: $O(V + E)$

### Optimal
- **Kahn's Algorithm (BFS)**:
  1. Build adjacency list `graph` and calculate `in_degree` for every course.
  2. Enqueue all courses with `in_degree == 0`.
  3. While queue is non-empty: pop course `u`, append to `order`, and decrement `in_degree` of each dependent course `v`.
  4. If `in_degree[v]` drops to 0, push `v` to queue.
  5. If `len(order) == numCourses`, return `order`; otherwise a cycle exists, return `[]`.

---

## Code (Python)

```python
from collections import deque
from typing import List

class Solution:
    def findOrder(self, numCourses: int, prerequisites: List[List[int]]) -> List[int]:
        # Build adjacency list and compute in-degrees
        adjacency_list = [[] for _ in range(numCourses)]
        in_degree = [0] * numCourses

        for course, prerequisite in prerequisites:
            adjacency_list[prerequisite].append(course)
            in_degree[course] += 1

        # Queue all nodes with zero in-degrees
        ready_queue = deque()
        for course_id in range(numCourses):
            if in_degree[course_id] == 0:
                ready_queue.append(course_id)

        topological_order = []

        # Process courses layer-by-layer
        while ready_queue:
            current_course = ready_queue.popleft()
            topological_order.append(current_course)

            for next_course in adjacency_list[current_course]:
                in_degree[next_course] -= 1
                # If all prerequisites are cleared, add to queue
                if in_degree[next_course] == 0:
                    ready_queue.append(next_course)

        # If topological order contains all courses, return it; else cycle exists
        if len(topological_order) == numCourses:
            return topological_order
        return []
```

---

## Dry Run (Smart Example)

Input: `numCourses = 4`, `prerequisites = [[1, 0], [2, 0], [3, 1], [3, 2]]`
Graph: `0 -> [1, 2]`, `1 -> [3]`, `2 -> [3]`. In-degrees: `[0:0, 1:1, 2:1, 3:2]`

| Step | Variables | Explanation |
| :--- | :--- | :--- |
| 1 | `queue=[0]`, `order=[]` | Course `0` has `in_degree == 0`; placed in queue. |
| 2 | `current=0`, `queue=[1, 2]`, `order=[0]` | Pop `0`. Decrement `in_degree` of `1` (becomes 0) and `2` (becomes 0). Enqueue both. |
| 3 | `current=1`, `queue=[2]`, `order=[0, 1]` | Pop `1`. Decrement `in_degree` of `3` from 2 to 1. `3` not ready yet. |
| 4 | `current=2`, `queue=[3]`, `order=[0, 1, 2]` | Pop `2`. Decrement `in_degree` of `3` from 1 to 0. Enqueue `3`. |
| 5 | `current=3`, `queue=[]`, `order=[0, 1, 2, 3]` | Pop `3`. Queue empty. `len(order) == 4 == numCourses`. Return valid order. |

---

## Edge Cases

- **No prerequisites (`prerequisites = []`)**: All nodes have in-degree 0; any order `[0, 1, ..., n-1]` is valid.
- **Cycle present (e.g., `[[0, 1], [1, 0]]`)**: Queue empties before all nodes visited; correctly returns `[]`.
- **Single course (`numCourses = 1, prerequisites = []`)**: Instantly returns `[0]`.
- **Disconnected components**: Independent graphs/isolated nodes get added via initial zero in-degree check seamlessly.

---

## Mistakes

- User Mistake: No specific note provided.
- Reversing edge directions accidentally: `[a, b]` means `b -> a` (must take `b` before `a`), not `a -> b`.
- Returning a partial list when a cycle exists instead of an empty list `[]`.
- Forgetting to check `len(topological_order) == numCourses` at the end to detect cycles.

---

## Complexity

Time: O(V + E) → Every vertex and prerequisite edge is processed at most once during graph construction and traversal.
Space: O(V + E) → Graph adjacency list takes O(E) space; queue, in-degree array, and result list take O(V) space.

---

## Similar Problems

- [Course Schedule](https://leetcode.com/problems/course-schedule/) - Medium
- [Alien Dictionary](https://leetcode.com/problems/alien-dictionary/) - Hard
- [Minimum Height Trees](https://leetcode.com/problems/minimum-height-trees/) - Medium
- [Sequence Reconstruction](https://leetcode.com/problems/sequence-reconstruction/) - Medium

---

## Tags and Properties

- #dsa #important #revisit #topologicalsort #bfs #graph #dag
- Concepts: [[Topological Sort]], [[Graph]], [[Kahn's Algorithm]], [[Breadth-First Search]]
- Last Reviewed: 2026-10-14
- Status: Ready for Revision
- **Problem Link:** [Course Schedule II - LeetCode](https://leetcode.com/problems/course-schedule-ii/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-10-16)
- [ ] Day 7 Revision (2026-10-21)
- [ ] Day 15 Revision (2026-10-29)
- [ ] Day 30 Revision (2026-11-13)
