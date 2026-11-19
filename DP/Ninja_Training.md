---
created: 2026-11-19
revisions:
  - 2026-11-21
  - 2026-11-26
  - 2026-12-04
  - 2026-12-19
---

# Ninja Training

---

## Metadata & Placement Tags

- **Folder:** DP
- **Target Companies:**
  - #Google #Amazon #Microsoft #Flipkart
- **Confidence Checklist:**
  - [ ] Low
  - [ ] Medium
  - [ ] High
- **Concepts:**
  - #dp [[Dynamic Programming]], #multidimensional-dp [[2D Dynamic Programming]], #state-machine [[State Machine DP]]

## Pattern

2D DP (State Machine / Choice with Previous Constraint)

---
## Difficulty

Medium
#medium

---

## ⚡ Key Idea (Core Insight)

On day `d`, taking activity `act` depends exclusively on the maximum points earned on day `d - 1` across all activities *except* `act`. State transition only requires tracking the previous day's best alternative choices.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Maintain a size-3 array `dp` of max points per activity; for each day and each task, add today's points to `max(dp[other_tasks])`.

---

## Approach

### Brute Force
- Recursively explore all valid activity paths ensuring adjacent days have distinct tasks.
- Time Complexity: $O(3 \times 2^{N-1}) = O(2^N)$

### Better
- Memoize overlapping subproblems using a 2D table `memo[day][last_activity]`.
- Time Complexity: $O(N \times 4 \times 3) = O(N)$, Space: $O(N \times 4)$ + recursion stack.

### Optimal
- Iterative DP with state compression:
  1. Initialize `prev_dp` with the three activity points of Day 0.
  2. For each day from 1 to $N-1$, compute `curr_dp[task] = points[day][task] + max(prev_dp[other_task])`.
  3. Set `prev_dp = curr_dp`.
  4. Final answer is `max(prev_dp)`.

---

## Code (Python)

```python
class Solution:
    def maximumPoints(self, points: list[list[int]], n: int) -> int:
        # Base case: Points earned on Day 0 for each activity
        prev_points = [points[0][0], points[0][1], points[0][2]]

        # Transition across subsequent days
        for day in range(1, n):
            curr_points = [0, 0, 0]
            for current_task in range(3):
                # Find maximum points achievable from a different task yesterday
                max_previous = 0
                for prev_task in range(3):
                    if prev_task != current_task:
                        if prev_points[prev_task] > max_previous:
                            max_previous = prev_points[prev_task]

                curr_points[current_task] = points[day][current_task] + max_previous

            # Roll forward state to use O(1) auxiliary space
            prev_points = curr_points

        return max(prev_points)
```

---

## Dry Run (Smart Example)

Input: `points = [[10, 40, 70], [20, 50, 80], [30, 60, 90]]`, `n = 3`

| Step | Variables | Explanation |
| :--- | :--- | :--- |
| 1 | `day=0`, `prev=[10, 40, 70]` | Base cases initialized directly from Day 0 scores. |
| 2 | `day=1`, `curr=[20+70, 50+70, 80+40]` | Task 0: $20+\max(40,70)=90$; Task 1: $50+\max(10,70)=120$; Task 2: $80+\max(10,40)=120$. `prev=[90, 120, 120]`. |
| 3 | `day=2`, `curr=[30+120, 60+120, 90+120]` | Task 0: $30+\max(120,120)=150$; Task 1: $60+\max(90,120)=180$; Task 2: $90+\max(90,120)=210$. `prev=[150, 180, 210]`. |
| 4 | Output = $\max(150, 180, 210) = 210$ | Highest points earned ending with Task 2. |

---

## Edge Cases

- **$N = 1$:** Loop doesn't execute; returns maximum element of first day directly.
- **Identical rewards across activities on a day:** Transition still valid since it picks between alternate task indices.
- **Strictly decreasing point values per day:** Greedy fails, DP explores optimal historical trade-offs accurately.

---

## Mistakes

- User Mistake: No specific note provided.
- Greedy pitfall: Picking `max(points[day])` locally leads to suboptimal future choices.
- Overwriting `prev_points` in-place while still computing other tasks for the current day.

---

## Complexity

Time: O(N) → Iterates $N-1$ days with a fixed $3 \times 2$ choice evaluations per day.
Space: O(1) → Stores state for only 3 activities across adjacent days.

---

## Similar Problems

- [House Robber](https://leetcode.com/problems/house-robber/) - Medium
- [Paint House](https://leetcode.com/problems/paint-house/) - Medium
- [Maximum Alternating Subsequence Sum](https://leetcode.com/problems/maximum-alternating-subsequence-sum/) - Medium
- [Best Time to Buy and Sell Stock with Cooldown](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-with-cooldown/) - Medium

---

## Tags and Properties

- #dsa #important #revisit #dynamicprogramming #statemachine #optimization
- [[Dynamic Programming]] [[Space Optimization]] [[State Machine]]
- **Revision Date:** 2026-11-19
- **Problem Link:** [GeeksforGeeks - Geek's Training / Ninja Training](https://www.geeksforgeeks.org/problems/geeks-training/1)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-11-21)
- [ ] Day 7 Revision (2026-11-26)
- [ ] Day 15 Revision (2026-12-04)
- [ ] Day 30 Revision (2026-12-19)
