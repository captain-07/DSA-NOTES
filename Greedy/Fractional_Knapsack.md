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

- **Folder:** Greedy
- **Target Companies:** #Amazon #Microsoft #Flipkart #Adobe #Paytm
- **Confidence Checklist:**
  - [ ] Low
  - [ ] Medium
  - [ ] High

- **Concepts:**
  - #greedy [[Greedy]], #sorting [[Sorting]], #heap [[Heaps]]

## Pattern

Greedy + Sorting (by Value-to-Weight Ratio)

---
## Difficulty

Medium
Tag: #medium

---

## ⚡ Key Idea (Core Insight)

- Calculate the value-to-weight ratio (`value / weight`) for each item.
- Sort items in descending order of this ratio and pick items greedily.
- If an item cannot fit completely into the remaining capacity, take the fraction of it that fits.

---

## ⚡ Quick Recall (VERY IMPORTANT)

- Sort by ratio `v/w` descending. Take full items until capacity runs out, then take the partial fraction of the next item.

---

## Approach

### Brute Force
- Try all combinations of subsets and fractions using continuous search/backtracking.
- Time Complexity: O(2^N) or unbounded continuous search.

### Optimal
- Compute ratio for all items, sort in descending order.
- Iterate through sorted items, adding whole items to the knapsack until capacity is exceeded.
- Fill remaining capacity with a fraction of the current item and terminate.

---

## Code (Python)

```python
class Item:
    def __init__(self, value: int, weight: int):
        self.value = value
        self.weight = weight

class Solution:
    def fractional_knapsack(self, capacity: int, values: list[int], weights: list[int]) -> float:
        # Create list of items
        items = []
        for index in range(len(values)):
            items.append(Item(values[index], weights[index]))

        # Sort items based on value-to-weight ratio in descending order
        items.sort(key=lambda item: item.value / item.weight, reverse=True)

        total_value = 0.0
        current_capacity = capacity

        for item in items:
            # If full item can fit, take it entirely
            if item.weight <= current_capacity:
                current_capacity -= item.weight
                total_value += item.value
            else:
                # Take fractional part of the item to fill remaining capacity
                fraction = current_capacity / item.weight
                total_value += item.value * fraction
                current_capacity = 0
                break  # Knapsack is now full

        return total_value
```

---

## Dry Run (Smart Example)

Input: `values = [60, 100, 120]`, `weights = [10, 20, 30]`, `capacity = 50`
Ratios: Item 0 = 6.0, Item 1 = 5.0, Item 2 = 4.0

| Step | Variables | Explanation |
|---|---|---|
| 1 | `item=(60,10)`, `capacity=50`, `total_val=0.0` | Weight 10 <= 50. Take full item. `capacity` becomes 40, `total_val` becomes 60.0. |
| 2 | `item=(100,20)`, `capacity=40`, `total_val=60.0` | Weight 20 <= 40. Take full item. `capacity` becomes 20, `total_val` becomes 160.0. |
| 3 | `item=(120,30)`, `capacity=20`, `total_val=160.0` | Weight 30 > 20. Take fraction (20/30). `total_val` += 120 * (20/30) = 80. Total = 240.0. Break. |

---

## Edge Cases

- **Capacity is 0:** Loop doesn't add anything; returns `0.0`.
- **Total items weight <= Capacity:** All items fit completely; returns sum of all values.
- **Single Item:** Takes min of full weight or fraction of capacity.
- **Items with identical ratios:** Sorting handles ties consistently without changing result.

---

## Mistakes

- Direct and actionable
- MUST include user mistake: No specific note provided.
- Forgetting to sort by `value / weight` ratio instead of pure value or weight alone.
- Using integer division instead of floating point division for fractional parts.

---

## Complexity

Time: O(N log N) → Driven by the sorting step of N items.
Space: O(N) → Auxiliary memory to store item objects/ratios for sorting.

---

## Similar Problems

- [0/1 Knapsack Problem](https://practice.geeksforgeeks.org/problems/0-1-knapsack-problem0945/1) - Medium
- [Maximum Units on a Truck](https://leetcode.com/problems/maximum-units-on-a-truck/) - Easy
- [Partition Equal Subset Sum](https://leetcode.com/problems/partition-equal-subset-sum/) - Medium

---

## Tags and Properties

- #dsa #important #revisit
- #greedy #fractional-knapsack #sorting
- Obsidian links: [[Greedy]], [[Sorting]], [[Fractional Knapsack]]
- **Revision Date:** 2026-09-20
- **Problem Link:** [GeeksforGeeks - Fractional Knapsack](https://practice.geeksforgeeks.org/problems/fractional-knapsack-1587115620/1)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-09-22)
- [ ] Day 7 Revision (2026-09-27)
- [ ] Day 15 Revision (2026-10-05)
- [ ] Day 30 Revision (2026-10-20)
