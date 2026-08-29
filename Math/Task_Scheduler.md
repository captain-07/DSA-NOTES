---
created: 2026-08-29
revisions:
  - 2026-08-31
  - 2026-09-05
  - 2026-09-13
  - 2026-09-28
---

# Task Scheduler

---

## Metadata & Placement Tags

- **Target Companies:** #Amazon #Google #Microsoft #Facebook #Uber
- **Confidence Checklist:**
  - [ ] Low
  - [ ] Medium
  - [ ] High
- **Concepts:** #greedy [[Greedy]], #heap [[Heap]], #math [[Math]]

---
## Pattern

Greedy + Math Formula

---
## Difficulty

Medium
#medium

---
## ⚡ Key Idea (Core Insight)

The schedule length is bottlenecked by the task with the maximum frequency ($f_{\text{max}}$). Arranging these maximum frequency tasks with their required cooling interval $n$ creates "slots" that can be filled by other tasks.

---
## ⚡ Quick Recall (VERY IMPORTANT)

Answer is $\max(\text{len(tasks)}, (f_{\text{max}} - 1) \times (n + 1) + k)$, where $k$ is the count of tasks with frequency $f_{\text{max}}$.

---
## Approach

### Brute Force
Generate all permutations of tasks and idle states to find the shortest valid sequence.
Time Complexity: $O(N!)$

### Better
Simulate CPU cycles using a **Max Heap** to always execute the most frequent task, and a **Queue** to track tasks currently on cooldown.
Time Complexity: $O(N \log K)$ (where $K$ is the count of unique tasks)

### Optimal
Count task frequencies. The highest frequency $f_{\text{max}}$ defines $(f_{\text{max}} - 1)$ groups of size $(n + 1)$. The final group will contain the $k$ tasks that share the maximum frequency.
Time Complexity: $O(N)$ time, $O(1)$ space.

---
## Code (Python)

```python
from collections import Counter

class Solution:
    def leastInterval(self, tasks: list[str], n: int) -> int:
        # Count frequencies of all tasks
        counts = Counter(tasks)
        f_max = max(counts.values())

        # Count how many tasks share the maximum frequency
        k = sum(1 for count in counts.values() if count == f_max)

        # Return either calculated slots or actual task count if no idle slots are needed
        return max(len(tasks), (f_max - 1) * (n + 1) + k)
```

---
## Dry Run (Smart Example)

Input: `tasks = ["A","A","A","B","B"], n = 2`

| Step | Variables | Explanation |
| :--- | :--- | :--- |
| 1 | `counts = {'A': 3, 'B': 2}`<br>`f_max = 3`, `k = 1` | 'A' has the highest frequency (3). Only 'A' has this frequency. |
| 2 | `min_slots = (3 - 1) * (2 + 1) + 1 = 7` | Apply formula: $(f_{\text{max}} - 1) \times (n + 1) + k$. |
| 3 | `ans = max(5, 7) = 7` | 7 slots are needed. Visual layout: `A -> B -> idle -> A -> B -> idle -> A`. |

---
## Edge Cases

- **$n = 0$:** No cooling time; return `len(tasks)`.
- **All unique tasks:** No duplicate constraints; return `len(tasks)`.
- **Very large $n$:** Idle slots dominate; the formula $(f_{\text{max}} - 1) \times (n + 1) + k$ dictates the result.
- **No idle slots needed:** If other tasks exceed empty slots, return `len(tasks)`.

---
## Mistakes

- **Initial block:** Didn't understand anything or how to handle task cooling constraints.
- **Ignoring $k$:** Forgetting to add $k$ (tasks with frequency $f_{\text{max}}$) to the end of the formula.
- **Ignoring task count lower bound:** Forgetting to take the `max` with `len(tasks)` when no idle units are needed.

---
## Complexity

Time: O(N) → Single pass to count frequencies. Finding the max and sum takes $O(26) = O(1)$ time.
Space: O(1) → Auxiliary storage for frequencies is capped at $O(26)$ unique uppercase English letters.

---
## Similar Problems

- [Reorganize String](https://leetcode.com/problems/reorganize-string/) - Medium
- [Rearrange String k Distance Apart](https://leetcode.com/problems/rearrange-string-k-distance-apart/) - Hard
- [Schedule Course III](https://leetcode.com/problems/course-schedule-iii/) - Hard

---
## Tags and Properties

- #dsa #important #revisit #greedy #math
- [[Greedy]] [[Math]] [[Heap]]
- **Revision Date:** 2026-08-29
- **Problem Link:** [LeetCode - Task Scheduler](https://leetcode.com/problems/task-scheduler/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-08-31)
- [ ] Day 7 Revision (2026-09-05)
- [ ] Day 15 Revision (2026-09-13)
- [ ] Day 30 Revision (2026-09-28)
