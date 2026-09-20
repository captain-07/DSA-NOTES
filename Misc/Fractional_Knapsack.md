---
created: 2026-09-20
revisions:
  - 2026-09-22
  - 2026-09-27
  - 2026-10-05
  - 2026-10-20
---

# Fractional Knapsack

---

## Metadata & Placement Tags

- **Folder:** Misc
- **Target Companies:** #Amazon #Google #Microsoft #Flipkart #Adobe
- **Confidence Checklist:**
  - [ ] Low
  - [ ] Medium
  - [ ] High

- **Concepts:**
  - #greedy [[Greedy Algorithm]], #sorting [[Sorting]]

---
## Pattern

Greedy Strategy + Sorting (Value-to-Weight Ratio)

---
## Difficulty

Medium
#medium

---

## ⚡ Key Idea (Core Insight)

- Calculate the value-to-weight ratio for each item.
- Pick items in descending order of their ratio to maximize value per unit weight.
- If an item cannot fit completely, take the fraction that fills the remaining capacity.

---

## ⚡ Quick Recall (VERY IMPORTANT)

- Sort by `value / weight` descending. Take fully while capacity allows; take fraction for the last fitting item.

---

## Approach

### Brute Force
- Try all $2^N$ combinations of items and fractions using continuous recursive search.
- **Time Complexity:** $O(2^N)$ (Infinite search space theoretically without discretization)

### Optimal
- Calculate `ratio = value / weight` for each item.
- Sort items by `ratio` in descending order.
- Iterate through sorted items:
  1. If item weight $\le$ remaining capacity: add total value, reduce capacity by item weight.
  2. Else: add `remaining capacity * ratio` to total value and break.
- **Time Complexity:** $O(N \log N)$

---

## Code (Python)

```python
class Item:
    def __init__(self, value: int, weight: int):
        self.value = value
        self.weight = weight

class Solution:
    def fractionalKnapsack(self, capacity: int, values: list[int], weights: list[int]) -> float:
        # Step 1: Create items list paired with value-to-weight ratio
        items = []
        for i in range(len(values)):
            ratio = values[i] / weights[i]
            items.append((ratio, values[i], weights[i]))

        # Step 2: Sort items by ratio in descending order
        items.sort(key=lambda x: x[0], reverse=True)

        total_value = 0.0
        current_capacity = capacity

        # Step 3: Pick items greedily
        for ratio, value, weight in items:
            if current_capacity == 0:
                break

            if weight <= current_capacity:
                # Take whole item
                total_value += value
                current_capacity -= weight
            else:
                # Take fraction of the item
                total_value += ratio * current_capacity
                current_capacity = 0

        return total_value
```

---

## Dry Run (Smart Example)

Input: `capacity = 50`, `values = [60, 100, 120]`, `weights = [10, 20, 30]`
Ratios: Item 1 = 6.0, Item 2 = 5.0, Item 3 = 4.0

| Step | Variables | Explanation |
| :--- | :--- | :--- |
| 1 | `ratio=6.0`, `val=60`, `wt=10`, `cap=50` | `10 <= 50`: Take full Item 1. `total_val = 60`, `cap = 40`. |
| 2 | `ratio=5.0`, `val=100`, `wt=20`, `cap=40` | `20 <= 40`: Take full Item 2. `total_val = 60 + 100 = 160`, `cap = 20`. |
| 3 | `ratio=4.0`, `val=120`, `wt=30`, `cap=20` | `30 > 20`: Take fraction (20/30) of Item 3. `total_val += 4.0 * 20 = 240`, `cap = 0`. |

Total Value: `240.0`

---

## Edge Cases

- **Capacity is 0:** Return `0.0` immediately.
- **Single item weight > Capacity:** Take only the valid fraction.
- **All items fit:** Return sum of all values.
- **Identical ratios:** Sorting order among tied ratios does not affect total value accuracy.

---

## Mistakes

- Confusing Fractional Knapsack with 0/1 Knapsack (0/1 requires DP, Fractional uses Greedy).
- Forgetting to convert division to float leading to integer division truncations.
- User mistake: No specific note provided.

---

## Complexity

Time: $O(N \log N)$ → Sorting $N$ items dominates the time complexity.
Space: $O(N)$ → Extra space used to store items with their ratios.

---

## Similar Problems

- [0/1 Knapsack Problem](https://practice.geeksforgeeks.org/problems/0-1-knapsack-problem0917/1) - Medium
- [Maximum Units on a Truck](https://leetcode.com/problems/maximum-units-on-a-truck/) - Easy
- [Bag of Tokens](https://leetcode.com/problems/bag-of-tokens/) - Medium

---

## Tags and Properties

- #dsa #important #revisit
- #greedy #fractional-knapsack #sorting
- [[Greedy Algorithm]], [[Sorting]], [[Knapsack]]
- **Revision Date:** 2026-09-20
- **Problem Link:** [Fractional Knapsack - GeeksforGeeks](https://practice.geeksforgeeks.org/problems/fractional-knapsack-1587115620/1)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-09-22)
- [ ] Day 7 Revision (2026-09-27)
- [ ] Day 15 Revision (2026-10-05)
- [ ] Day 30 Revision (2026-10-20)
