---
created: 2026-09-21
revisions:
  - 2026-09-23
  - 2026-09-28
  - 2026-10-06
  - 2026-10-21
---

# Shortest Job First

---

## Metadata & Placement Tags

- **Folder:** Greedy
- **Target Companies:** #Amazon #Microsoft #Flipkart #Google
- **Confidence Checklist:**
  - [ ] Low
  - [ ] Medium
  - [ ] High

- **Concepts:**
  - #greedy [[Greedy]], #sorting [[Sorting]], #array [[Array]]

## Pattern

Sorting + Greedy

---
## Difficulty

Medium #medium

---

## ⚡ Key Idea (Core Insight)

To minimize the total waiting time, always process the process with the shortest burst time first (Shortest Job First scheduling). Sorting execution times in non-decreasing order ensures that shorter jobs reduce the waiting time overhead for all subsequent jobs.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Sort burst times ascending. Maintain `current_wait_time` (accumulated time spent waiting before current process) and add it to `total_wait_time` at each step.

---

## Approach

### Brute Force
- Try all permutations of process execution order to find the one with minimum total waiting time.
- Time Complexity: O(N!)
- Space Complexity: O(N)

### Optimal
- Sort burst times in non-decreasing order.
- Iterate through sorted burst times:
  1. Add `current_wait_time` to `total_wait_time`.
  2. Increase `current_wait_time` by the current process's burst time.
- Calculate average waiting time as `total_wait_time // N`.
- Time Complexity: O(N log N)
- Space Complexity: O(1) or O(N) depending on sort implementation.

---

## Code (Python)

```python
class Solution:
    def solve(self, bt: list[int]) -> int:
        # Sort burst times to execute shortest jobs first
        bt.sort()

        total_wait_time = 0
        current_wait_time = 0

        # Calculate waiting time for each process
        for burst_time in bt:
            # Add time waited by the current process before execution
            total_wait_time += current_wait_time
            # Increment elapsed time for the next process
            current_wait_time += burst_time

        # Return average waiting time (integer division)
        return total_wait_time // len(bt)
```

---

## Dry Run (Smart Example)

Input: `bt = [4, 3, 7, 1, 2]`
Sorted Input: `[1, 2, 3, 4, 7]`

| Step | Variables | Explanation |
| :--- | :--- | :--- |
| **Init** | `total_wait_time = 0`, `current_wait_time = 0` | Initial state |
| **1 (bt=1)** | `total_wait_time += 0` → `0`<br>`current_wait_time += 1` → `1` | Process 1 waits `0`. Elapsed time becomes `1`. |
| **2 (bt=2)** | `total_wait_time += 1` → `1`<br>`current_wait_time += 2` → `3` | Process 2 waits `1`. Elapsed time becomes `3`. |
| **3 (bt=3)** | `total_wait_time += 3` → `4`<br>`current_wait_time += 3` → `6` | Process 3 waits `3`. Elapsed time becomes `6`. |
| **4 (bt=4)** | `total_wait_time += 6` → `10`<br>`current_wait_time += 4` → `10` | Process 4 waits `6`. Elapsed time becomes `10`. |
| **5 (bt=7)** | `total_wait_time += 10` → `20`<br>`current_wait_time += 7` → `17` | Process 5 waits `10`. Elapsed time becomes `17`. |
| **Final** | `20 // 5` → `4` | Average waiting time is `4`. |

---

## Edge Cases

- **Single Process (`bt = [5]`):** Waiting time is `0`. Handled correctly (`0 // 1 = 0`).
- **All Identical Elements (`bt = [2, 2, 2]`):** Order doesn't matter; accumulated correctly.
- **Large Input Values:** Ensure `total_wait_time` accumulator does not overflow (Python handles arbitrary-precision integers natively).

---

## Mistakes

- Adding burst time directly to `total_wait_time` instead of tracking elapsed time.
- **Main Funda:** The main funda is to keep track of current waiting time along with the total waiting time.
- Forgetting to return integer division (floor value) as per standard problem requirements.

---

## Complexity

Time: O(N log N) → Dominated by sorting the burst time array.
Space: O(1) → In-place sort (or O(N) depending on language sorting allocation).

---

## Similar Problems

- [Minimum Number of Taps to Open to Water a Garden](https://leetcode.com/problems/minimum-number-of-taps-to-open-to-water-a-garden/) - Hard
- [Assign Cookies](https://leetcode.com/problems/assign-cookies/) - Easy
- [Shortest Job First (CPU Scheduling)](https://www.geeksforgeeks.org/problems/shortest-job-first/1) - Medium

---

## Tags and Properties

- #dsa #important #revisit
- #greedy #cpu-scheduling [[Greedy Algorithms]], [[Sorting]]
- **Last Revised:** 2026-09-21
- **Problem Link:** [GeeksforGeeks - Shortest Job First](https://www.geeksforgeeks.org/problems/shortest-job-first/1)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-09-23)
- [ ] Day 7 Revision (2026-09-28)
- [ ] Day 15 Revision (2026-10-06)
- [ ] Day 30 Revision (2026-10-21)
