---
created: 2026-09-22
revisions:
  - 2026-09-24
  - 2026-09-29
  - 2026-10-07
  - 2026-10-22
---

# Job Sequencing Problem

---

## Metadata & Placement Tags

- **Folder:** Greedy
- **Target Companies:** #Amazon #Microsoft #Flipkart #Directi
- **Confidence Checklist:**
  - [ ] Low
  - [ ] Medium
  - [ ] High

- **Concepts:**
  - #greedy [[Greedy]], #disjointset [[Disjoint Set Union]], #sorting [[Sorting]]

## Pattern

Greedy + Disjoint Set Union (DSU) / Slot Finding

---
## Difficulty

Medium
Tag: #medium

---

## ⚡ Key Idea (Core Insight)

To maximize total profit, sort jobs by profit in descending order and greedily schedule each job on the latest available time slot before or on its deadline. Using DSU speeds up finding the latest available slot in $O(\alpha(N))$ time instead of linear search.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Sort by profit descending. Place job at deadline slot; if occupied, use DSU parent pointer to jump instantly to the next available earlier slot.

---

## Approach

### Brute Force
- Iterate over each job (sorted by profit) and search linearly backwards from `min(max_deadline, deadline)` to 1 to find an empty slot.
- Time Complexity: $O(N \log N + N \times \text{max\_deadline})$ | Space: $O(\text{max\_deadline})$

### Optimal (DSU)
- Sort jobs by profit descending.
- Initialize DSU where each slot points to itself.
- For each job with `deadline`, find its representative parent `available_slot`. If `available_slot > 0`, schedule the job and union `available_slot` with `available_slot - 1`.

---

## Code (Python)

```python
class Job:
    def __init__(self, job_id, deadline, profit):
        self.id = job_id
        self.deadline = deadline
        self.profit = profit

class Solution:
    def find_parent(self, parent, i):
        # Path compression
        if parent[i] == i:
            return i
        parent[i] = self.find_parent(parent, parent[i])
        return parent[i]

    def JobScheduling(self, jobs, n):
        # Sort jobs based on profit in descending order
        jobs.sort(key=lambda x: x.profit, reverse=True)

        # Find maximum deadline to size DSU table
        max_deadline = max(job.deadline for job in jobs)

        # Initialize parent array for DSU (1-indexed up to max_deadline)
        parent = [i for i in range(max_deadline + 1)]

        count_jobs = 0
        total_profit = 0

        for job in jobs:
            # Find latest available slot <= job.deadline
            available_slot = self.find_parent(parent, min(max_deadline, job.deadline))

            # If slot > 0, we can schedule this job
            if available_slot > 0:
                count_jobs += 1
                total_profit += job.profit
                # Merge current slot with available slot on the left
                parent[available_slot] = self.find_parent(parent, available_slot - 1)

        return [count_jobs, total_profit]
```

---

## Dry Run (Smart Example)

Input Jobs: `[(1, 4, 20), (2, 1, 10), (3, 1, 40), (4, 1, 30)]`
Sorted by profit: `J3(d=1, p=40), J4(d=1, p=30), J1(d=4, p=20), J2(d=1, p=10)`
`max_deadline = 4`, DSU `parent = [0, 1, 2, 3, 4]`

| Step | Current Job | Available Slot (find) | Action & DSU Update | Count / Profit |
| :--- | :--- | :--- | :--- | :--- |
| 1 | J3 (deadline=1, profit=40) | 1 | Occupy slot 1. Union(1, 0) -> `parent[1]=0`. | Count=1, Profit=40 |
| 2 | J4 (deadline=1, profit=30) | 0 (`find(1)` -> 0) | Slot 0 invalid. Skip job. | Count=1, Profit=40 |
| 3 | J1 (deadline=4, profit=20) | 4 | Occupy slot 4. Union(4, 3) -> `parent[4]=3`. | Count=2, Profit=60 |
| 4 | J2 (deadline=1, profit=10) | 0 (`find(1)` -> 0) | Slot 0 invalid. Skip job. | Count=2, Profit=60 |

---

## Edge Cases

- **All deadlines are 1:** Only one highest-profit job can be completed.
- **Deadlines larger than total jobs:** Handled smoothly by limiting slots to `max_deadline`.
- **Jobs with duplicate profits/deadlines:** Handled correctly via strict descending sort order.
- **Single job:** Processed in 1 step, returns `[1, profit]`.

---

## Mistakes

- Using two `for` loops (linear backward scan) is intuitive, but fails to reach optimal time complexity; use DSU for $O(\alpha(N))$ slot lookup.
- Allocating array indexed by job count instead of `max_deadline`.
- Forgetting path compression in DSU, degenerating performance to linear time.

---

## Complexity

Time: $O(N \log N + N \cdot \alpha(M))$ → Sorting takes $O(N \log N)$ and DSU find operations take near-constant time $O(\alpha(M))$ where $M$ is max deadline.
Space: $O(M)$ → DSU parent array of size `max_deadline + 1`.

---

## Similar Problems

- [Task Scheduler](https://leetcode.com/problems/task-scheduler/) - Medium
- [Maximum Profit in Job Scheduling](https://leetcode.com/problems/maximum-profit-in-job-scheduling/) - Hard
- [Course Schedule III](https://leetcode.com/problems/course-schedule-iii/) - Hard

---

## Tags and Properties

- #dsa #important #revisit
- #greedy [[Greedy]] #disjointset [[Disjoint Set Union]]
- **Revision Date:** 2026-09-22
- **Problem Link:** [Job Sequencing Problem - GeeksforGeeks](https://www.geeksforgeeks.org/problems/job-sequencing-problem-1587115620/1)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-09-24)
- [ ] Day 7 Revision (2026-09-29)
- [ ] Day 15 Revision (2026-10-07)
- [ ] Day 30 Revision (2026-10-22)
