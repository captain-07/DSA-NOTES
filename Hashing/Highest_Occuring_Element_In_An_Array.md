---
created: 2026-04-07
revisions:
  - 2026-04-09
  - 2026-04-14
  - 2026-04-22
  - 2026-05-07
---

# Highest Occuring Element In An Array

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Google #Microsoft #Adobe #TCS #Infosys

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #hashmap [[HashMap]], #arrays [[Arrays]], #counting [[Counting]]

---
## Pattern

Frequency Counting + HashMap Iteration  

---
## Difficulty

Easy  
#easy

---

## ⚡ Key Idea (Core Insight)

Use a hash map (dictionary) to store the frequency of each element while traversing the array once. Then, identify the key with the maximum value.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Map each element to its count; return the key associated with the `max()` value in the map.

---

## Approach

### Brute Force
- Use nested loops: for each element, count its occurrences in the rest of the array.
- Time Complexity: O(N²)

### Better
- Sort the array first. Identical elements will be adjacent. Count contiguous blocks.
- Time Complexity: O(N log N) | Space: O(1) (ignoring sorting overhead)

### Optimal
- **Step 1:** Initialize an empty hash map (dictionary).
- **Step 2:** Iterate through the array; increment the count for each element in the map.
- **Step 3:** Keep track of the `max_freq` and corresponding `result_element` during the single pass to avoid a second loop.

---

## Code (Python)

```python
def get_highest_occurring_element(nums):
    # Dictionary to store frequency of each element
    counts = {}
    max_freq = 0
    result = None
    
    for num in nums:
        # Update frequency count
        counts[num] = counts.get(num, 0) + 1
        
        # Update result if current element's frequency is higher
        if counts[num] > max_freq:
            max_freq = counts[num]
            result = num
            
    return result

# Example usage:
# arr = [1, 3, 2, 1, 4, 1, 2]
# print(get_highest_occurring_element(arr)) # Output: 1
```

---

## Dry Run (Smart Example)

Input: `nums = [2, 3, 2, 1, 3, 3]`

| Step | Element | HashMap State | max_freq | result | Explanation |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | 2 | `{2: 1}` | 1 | 2 | First seen, set freq to 1. |
| 2 | 3 | `{2: 1, 3: 1}` | 1 | 2 | Freq 1 is not > max_freq. |
| 3 | 2 | `{2: 2, 3: 1}` | 2 | 2 | Freq of 2 becomes 2, update result. |
| 4 | 1 | `{2: 2, 3: 1, 1: 1}` | 2 | 2 | Freq 1 is not > max_freq. |
| 5 | 3 | `{2: 2, 3: 2, 1: 1}` | 2 | 2 | Freq of 3 is 2 (not > max_freq). |
| 6 | 3 | `{2: 2, 3: 3, 1: 1}` | 3 | 3 | Freq of 3 becomes 3, update result. |

---

## Edge Cases

- **Empty Array:** Should handle or return `None`.
- **Single Element:** The element itself is the highest occurring.
- **All Unique Elements:** Any element could be returned (usually the first).
- **Multiple Elements with Same Max Frequency:** Return the first encountered or as specified by the problem.
- **Negative Numbers:** HashMap handles these naturally as keys.

---

## Mistakes

- Using O(N²) nested loops when O(N) is possible.
- Forgetting to handle the case where the input array is empty.
- Recalculating `max(counts.values())` inside the loop (inefficient).
- **User Mistake:** No specific note provided.

---

## Complexity

Time: O(N) → We traverse the array exactly once to build the frequency map.  
Space: O(N) → In the worst case (all unique elements), the hash map stores N entries.

---

## Similar Problems

- [Majority Element ( > N/2 times)](https://leetcode.com/problems/majority-element/) - Easy
- [Top K Frequent Elements](https://leetcode.com/problems/top-k-frequent-elements/) - Medium
- [Sort Characters By Frequency](https://leetcode.com/problems/sort-characters-by-frequency/) - Medium
- [Find All Duplicates in an Array](https://leetcode.com/problems/find-all-duplicates-in-an-array/) - Medium

---

## Tags and Properties

- #dsa #important #revisit #arrays #hashmap
- [[HashMap]] [[Counting]] [[Frequency Analysis]]
- **Revision Date:** 2026-04-07
- **Problem Link:** [Majority Element (Related)](https://leetcode.com/problems/majority-element/) | [Find Mode in Binary Search Tree](https://leetcode.com/problems/find-mode-in-binary-search-tree/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-09)
- [ ] Day 7 Revision (2026-04-14)
- [ ] Day 15 Revision (2026-04-22)
- [ ] Day 30 Revision (2026-05-07)
