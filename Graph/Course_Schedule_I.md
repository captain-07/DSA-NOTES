---
created: 2026-10-14
revisions:
  - 2026-10-16
  - 2026-10-21
  - 2026-10-29
  - 2026-11-13
---

# Course Schedule I

---

## Metadata & Placement Tags

- **Folder:** Graph
- **Target Companies:** #Amazon #Google #Microsoft #Meta #Uber
- **Confidence Checklist:**
  - [ ] Low
  - [ ] Medium
  - [ ] High
- **Concepts:**
  - #graph [[Graph]], #topological-sort [[Topological Sort]], #bfs [[Breadth-First Search]], #dfs [[Depth-First Search]], #cycle-detection [[Cycle Detection]]

## Pattern

Topological Sort (Kahn's Algorithm / BFS) or Directed Cycle Detection (DFS 3-Coloring)

---
## Difficulty

Medium
#medium

---

## ⚡ Key Idea (Core Insight)

Treat courses as directed edges `[u, v]` where `v -> u`. Finishing all courses is possible **if and only if the directed graph contains no directed cycle**.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Build adjacency list + indegree array. Push 0-indegree nodes to queue (Kahn's BFS); if processed count == `numCourses`, return `True`, else `False`.

---

## Approach

### Brute Force
- Find all possible paths from each node and check if any node revisits itself along the current path.
- Complexity: O(V * V!) or O(V * 2^V) time.

### Better
- **DFS with Visited States (3-Coloring):**
  - Unvisited (0), Visiting (1), Visited (2). If DFS encounters a node in state 1, a back-edge/cycle exists.
  - Complexity: O(V + E) time, O(V + E) space.

### Optimal
- **Kahn's Algorithm (BFS via Indegrees):**
  - Step 1: Compute `in_degree` for every course and build adjacency list `graph`.
  - Step 2: Push all courses with `in_degree == 0` into a queue.
  - Step 3: Pop course, increment `processed_count`, reduce `in_degree` of its neighbors. If neighbor's `in_degree` hits 0, enqueue it.
  - Step 4: Return `processed_count == numCourses`.

---

## Code (Python)

### Optimal Solution 1: Kahn's Algorithm (BFS)

```python
from collections import deque

class Solution:
    def canFinish(self, numCourses: int, prerequisites: list[list[int]]) -> bool:
        # Build adjacency list and indegree tracker
        adjacency_list = [[] for _ in range(numCourses)]
        in_degree = [0] * numCourses

        for course, prereq in prerequisites:
            adjacency_list[prereq].append(course)
            in_degree[course] += 1

        # Queue nodes with 0 incoming dependencies
        queue = deque()
        for course_id in range(numCourses):
            if in_degree[course_id] == 0:
                queue.append(course_id)

        completed_courses = 0

        while queue:
            current_course = queue.popleft()
            completed_courses += 1

            # Decrement dependency count for downstream courses
            for next_course in adjacency_list[current_course]:
                in_degree[next_course] -= 1
                if in_degree[next_course] == 0:
                    queue.append(next_course)

        return completed_courses == numCourses
```

### Optimal Solution 2: DFS 3-Coloring (Cycle Detection)

```python
class Solution:
    def _has_cycle(self, course: int, adjacency_list: list[list[int]], state: list[int]) -> bool:
        # State: 0 = unvisited, 1 = visiting (in recursion stack), 2 = visited
        if state[course] == 1:
            return True  # Found cycle
        if state[course] == 2:
            return False  # Already verified cycle-free

        state[course] = 1
        for next_course in adjacency_list[course]:
            if self._has_cycle(next_course, adjacency_list, state):
                return True
        state[course] = 2

        return False

    def canFinish(self, numCourses: int, prerequisites: list[list[int]]) -> bool:
        adjacency_list = [[] for _ in range(numCourses)]
        for course, prereq in prerequisites:
            adjacency_list[prereq].append(course)

        state = [0] * numCourses
        for course_id in range(numCourses):
            if state[course_id] == 0:
                if self._has_cycle(course_id, adjacency_list, state):
                    return False

        return True
```

---

## Dry Run (Smart Example)

Input: `numCourses = 4`, `prerequisites = [[1, 0], [2, 1], [3, 2], [1, 3]]` (Cycle `1 -> 2 -> 3 -> 1`)

| Step | Queue | Processed / `in_degree` State | Explanation |
| :--- | :--- | :--- | :--- |
| **0** | `[0]` | `in_degree = [0, 2, 1, 1]`, `completed = 0` | Node 0 has 0 indegree; pushed to queue. |
| **1** | `[]` | `current = 0`, `completed = 1`, `in_degree[1] = 1` | Pop 0; decrement neighbor 1's indegree from 2 to 1 (not 0). |
| **2** | `[]` | `queue is empty`, `completed = 1` | Queue empty; loop terminates because nodes 1, 2, 3 have indegree > 0. |
| **3** | End | `completed (1) != numCourses (4)` | Returns `False` due to deadlocked cycle. |

---

## Edge Cases

- **No prerequisites (`[]`):** Every node starts with `in_degree == 0`, immediately returns `True`.
- **Disconnected components with a cycle in one:** Must run cycle detection/indegree across all components.
- **Direct 2-node cycle (`[[0, 1], [1, 0]]`):** Neither node has indegree 0, queue starts empty, returns `False`.
- **Multiple parallel prerequisites:** Correctly increments indegrees without breaking queue logic.

---

## Mistakes

- User Mistake: No specific note provided.
- Reversing edge direction (`course -> prereq` vs `prereq -> course`) leading to inverted topological logic.
- Using simple boolean `visited` in DFS instead of 3-state tracking (wrongly flags cross-edges as cycles).
- Forgetting to check if `completed_courses == numCourses` at the end of Kahn's BFS.

---

## Complexity

Time: O(V + E) → Each vertex and directed edge is traversed exactly once.
Space: O(V + E) → Storage for adjacency list, indegree/state array, and queue/call-stack.

---

## Similar Problems

- [Course Schedule II](https://leetcode.com/problems/course-schedule-ii/) - Medium
- [Alien Dictionary](https://leetcode.com/problems/alien-dictionary/) - Hard
- [Minimum Height Trees](https://leetcode.com/problems/minimum-height-trees/) - Medium
- [Course Schedule IV](https://leetcode.com/problems/course-schedule-iv/) - Medium

---

## Tags and Properties

- #dsa #important #revisit #topological-sort #graph #bfs #dfs
- [[Graph]], [[Topological Sort]], [[Breadth-First Search]], [[Cycle Detection]]
- **Last Revised:** 2026-10-14
- **Problem Link:** [LeetCode - Course Schedule](https://leetcode.com/problems/course-schedule/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-10-16)
- [ ] Day 7 Revision (2026-10-21)
- [ ] Day 15 Revision (2026-10-29)
- [ ] Day 30 Revision (2026-11-13)
