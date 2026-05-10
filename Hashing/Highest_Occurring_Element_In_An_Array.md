---
created: 2026-04-10
revisions:
  - 2026-04-12
  - 2026-04-17
  - 2026-04-25
  - 2026-05-10
---

# Highest Occuring Element In An Array

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Google #Microsoft #Adobe #Samsung

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #hashmap [[HashMap]], #frequency-counting [[Frequency Counting]], #sorting [[Sorting]]

## Pattern

HashMap / Frequency Array  
Sorting + Linear Scan

---
## Difficulty

Easy  
#easy

---

## ⚡ Key Idea (Core Insight)

- Use a **HashMap** to store the frequency of each element as you traverse the array.
- Maintain a `max_count` variable and a `result` variable to track the element with the highest frequency in a single pass.

---

## ⚡ Quick Recall (VERY IMPORTANT)

- Count frequencies using a Map; return the key with the maximum value.

---

## Approach

### Brute Force
- Use nested loops to count occurrences of each element one by one.
- **Time Complexity:** O(N²)

### Better
- Sort the array first. Identical elements will be adjacent. Count the longest consecutive streak.
- **Time Complexity:** O(N log N) (due to sorting)

### Optimal
- Use a Hash Map (Dictionary in Python) to store `{element: count}`.
- Iterate through the array once to populate the map and update the leader.
- **Time Complexity:** O(N)
- **Space Complexity:** O(N)

---

## Code (Python)

```python
class Solution:
    def highestOccurringElement(self, nums: list[int]) -> int:
        # Dictionary to store frequency of each element
        frequency_map = {}
        max_count = 0
        result = nums[0]

        for num in nums:
            # Increment frequency
            frequency_map[num] = frequency_map.get(num, 0) + 1
            
            # Update result if current element's frequency is higher
            if frequency_map[num] > max_count:
                max_count = frequency_map[num]
                result = num
            # Optional: Handle tie-breaking (e.g., smallest element) if required
            elif frequency_map[num] == max_count:
                result = min(result, num)
                
        return result
```

---

## Dry Run (Smart Example)

Input: `nums = [1, 3, 2, 3, 4, 1, 3]`

| Step | Current Num | frequency_map | max_count | result | Explanation |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | 1 | `{1: 1}` | 1 | 1 | First element. |
| 2 | 3 | `{1: 1, 3: 1}` | 1 | 1 | Tie at 1, result stays 1 (or updates based on logic). |
| 3 | 2 | `{1: 1, 3: 1, 2: 1}` | 1 | 1 | No change in max_count. |
| 4 | 3 | `{1: 1, 3: 2, 2: 1}` | 2 | 3 | 3 becomes the most frequent. |
| 5 | 4 | `{... 4: 1}` | 2 | 3 | No change. |
| 6 | 1 | `{1: 2, 3: 2, ...}` | 2 | 3 | Tie at 2. result stays 3 (logic dependent). |
| 7 | 3 | `{1: 2, 3: 3, ...}` | 3 | 3 | 3 is final winner. |

---

## Edge Cases

- **Empty Array:** Should return null or handle based on constraints.
- **Single Element:** The element itself is the highest occurring.
- **All Elements Unique:** Any element is technically correct (usually the first or smallest).
- **Multiple Elements with Same Max Frequency:** Clarify if the problem asks for the first one, the smallest one, or any.
- **Negative Numbers:** HashMap handles these naturally.

---

## Mistakes

- Using a nested loop (O(N²)) when a HashMap (O(N)) is available.
- Forgetting to handle ties if the problem specifies a tie-breaking rule.
- Initializing `max_count` incorrectly (should be 0 or frequency of first element).
- **User Mistake:** No specific note provided.

---

## Complexity

Time: O(N) → Single pass to build the map and track the maximum frequency.  
Space: O(N) → In the worst case (all elements unique), the map stores N entries.

---

## Similar Problems

- [Majority Element](https://leetcode.com/problems/majority-element/) - Easy
- [Top K Frequent Elements](https://leetcode.com/problems/top-k-frequent-elements/) - Medium
- [Sort Characters By Frequency](https://leetcode.com/problems/sort-characters-by-frequency/) - Medium
- [Find Lucky Integer in an Array](https://leetcode.com/problems/find-lucky-integer-in-an-array/) - Easy

---

## Tags and Properties
  - #dsa #important #revisit #arrays #hashmap
  - [[HashMap]] [[Frequency Counting]]
  - **Revision Date:** 2026-04-10
  - **Problem Link:** [Majority Element (LC #169)](https://leetcode.com/problems/majority-element/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-12)
- [ ] Day 7 Revision (2026-04-17)
- [ ] Day 15 Revision (2026-04-25)
- [ ] Day 30 Revision (2026-05-10)
