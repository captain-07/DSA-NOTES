---
created: 2026-04-25
revisions:
  - 2026-04-27
  - 2026-05-02
  - 2026-05-10
  - 2026-05-25
---

# Stock Buy And Sell

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Microsoft #Google #Adobe #GoldmanSachs #Facebook

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #array [[Array]]
  - #greedy [[Greedy]]
  - #dynamicprogramming [[Dynamic Programming]]

## Pattern
Sliding Window / Single Pass Greedy

---
## Difficulty
Easy
#easy

---

## ⚡ Key Idea (Core Insight)
To maximize profit, you must **buy at the lowest possible price** seen so far and **sell at the current price**. You only need to track the minimum price encountered while iterating through the array once.

---

## ⚡ Quick Recall (VERY IMPORTANT)
Maintain `min_price` and `max_profit`. For every price: update `min_price`, calculate `current_profit`, and update `max_profit`.

---

## Approach

### Brute Force
- Iterate through every pair `(i, j)` where `j > i` and calculate `prices[j] - prices[i]`.
- Time Complexity: O(N²)

### Better
- Not applicable for this specific problem (the jump from O(N²) to O(N) is direct).

### Optimal (Single Pass)
1. Initialize `min_price` to infinity and `max_profit` to 0.
2. Traverse the array:
   - Update `min_price` if the current price is lower.
   - Else, calculate `profit = current_price - min_price` and update `max_profit`.
3. Return `max_profit`.

---

## Code (Python)

```python
class Solution:
    def maxProfit(self, prices: list[int]) -> int:
        # Initialize min_price to a very large value
        min_price = float('inf')
        max_profit = 0
        
        for price in prices:
            # Update the minimum price seen so far
            if price < min_price:
                min_price = price
            # Calculate potential profit if sold today
            elif price - min_price > max_profit:
                max_profit = price - min_price
                
        return max_profit
```

---

## Dry Run (Smart Example)
Input: `prices = [3, 2, 6, 5, 0, 3]`

| Step | Price | min_price | Profit (Price - min) | max_profit | Explanation |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | 3 | 3 | 0 | 0 | Initialize min_price to 3 |
| 2 | 2 | 2 | 0 | 0 | Update min_price to 2 |
| 3 | 6 | 2 | 4 | 4 | Sell at 6, buy at 2 |
| 4 | 5 | 2 | 3 | 4 | Profit 3 < max_profit 4 |
| 5 | 0 | 0 | 0 | 4 | Update min_price to 0 |
| 6 | 3 | 0 | 3 | 4 | Profit 3 < max_profit 4 |

---

## Edge Cases
- **Descending Prices:** `[5, 4, 3, 2, 1]` -> `max_profit` remains 0.
- **Single Price:** `[5]` -> Cannot buy and sell, profit 0.
- **Constant Prices:** `[3, 3, 3]` -> Profit 0.
- **Empty Array:** `[]` -> Return 0.

---

## Mistakes
- Trying to buy and sell on the same day (should be different days).
- Forgetting to reset `min_price` or initializing `max_profit` with a negative number (profit cannot be negative here; 0 is the floor).
- **User Mistake:** No specific note provided.

---

## Complexity
Time: O(N) → Single traversal of the price array.  
Space: O(1) → Only two variables used regardless of input size.

---

## Similar Problems
- [Best Time to Buy and Sell Stock II](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-ii/) - Medium
- [Best Time to Buy and Sell Stock III](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-iii/) - Hard
- [Maximum Subarray (Kadane's)](https://leetcode.com/problems/maximum-subarray/) - Medium

---

## Tags and Properties
- #dsa #important #revisit #greedy #stock
- [[Array]] [[Greedy]]
- Revision Date: 2026-04-25
- **Problem Link:** [LeetCode - Best Time to Buy and Sell Stock](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-27)
- [ ] Day 7 Revision (2026-05-02)
- [ ] Day 15 Revision (2026-05-10)
- [ ] Day 30 Revision (2026-05-25)
