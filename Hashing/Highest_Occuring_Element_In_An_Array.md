---
created: 2026-04-06
revisions:
  - 2026-04-08
  - 2026-04-13
  - 2026-04-21
  - 2026-05-06
---

# Highest Occuring Element In An Array

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Google #Microsoft #Adobe #TCS

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #hashmap [[HashMap]]
  - #array [[Array]]
  - #sorting [[Sorting]]

---
## Pattern

HashMap Frequency Counting  
Sorting + Linear Scan

---
## Difficulty

Easy  
#easy

---

## ⚡ Key Idea (Core Insight)

The most efficient way to find the mode (highest occurring element) is to use a **Frequency Map**. By mapping each unique element to its count, we can determine the maximum frequency in a single pass after or during the counting process.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Use a `dictionary` to count occurrences. Iterate through the map to find the key with the largest value.

---

## Approach

### Brute Force
- Use nested loops: for each element, count its occurrences by scanning the rest of the array.
- **Time Complexity:** $O(N^2)$
- **Space Complexity:** $O(1)$

### Better
- Sort the array first. Identical elements will be adjacent. Count consecutive elements and keep track of the maximum streak.
- **Time Complexity:** $O(N \log N)$ (due to sorting)
- **Space Complexity:** $O(1)$ or $O(N)$ depending on sort implementation.

### Optimal
1. Initialize an empty HashMap (dictionary).
2. Traverse the array:
   - If element exists in map, increment count.
   - Else, add element to map with count 1.
3. Keep a `max_element` and `max_count` variable to update during the traversal to avoid a second pass.
- **Time Complexity:** $O(N)$
- **Space Complexity:** $O(N)$

---

## Code (Python)

```python
def highest_occurring_element(arr):
    if not arr:
        return None
        
    frequency = {}
    max_element = arr[0]
    max_count = 0
    
    for num in arr:
        # Update frequency count
        frequency[num] = frequency.get(num, 0) + 1
        
        # Track the element with the highest frequency
        if frequency[num] > max_count:
            max_count = frequency[num]
            max_element = num
            
    return max_element

# Alternative using Collections (Interview tip)
from collections import Counter
def highest_occurring_easy(arr):
    if not arr: return None
    # Returns the most common element and its count
    return Counter(arr).most_common(1)[0][0]
```

---

## Dry Run (Smart Example)

**Input:** `[1, 3, 2, 3, 1, 3]`

| Step | Num | Frequency Map | max_element | max_count | Explanation |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | 1 | `{1: 1}` | 1 | 1 | First element encountered. |
| 2 | 3 | `{1: 1, 3: 1}` | 1 | 1 | 3 added, count not greater than 1. |
| 3 | 2 | `{1: 1, 3: 1, 2: 1}` | 1 | 1 | 2 added, count not greater than 1. |
| 4 | 3 | `{1: 1, 3: 2, 2: 1}` | 3 | 2 | 3 count becomes 2; updates max. |
| 5 | 1 | `{1: 2, 3: 2, 2: 1}` | 3 | 2 | 1 count becomes 2; doesn't exceed 3's count. |
| 6 | 3 | `{1: 2, 3: 3, 2: 1}` | 3 | 3 | 3 count becomes 3; updates max. |

---

## Edge Cases

- **Empty Array:** Should return `None` or handle gracefully.
- **Single Element:** The element itself is the highest occurring.
- **All Elements Unique:** Any element can be returned (usually the first one).
- **Multiple Modes:** (e.g., two 3s and two 4s) Usually return the first one encountered or as per specific requirements.
- **Negative Numbers:** HashMap handles these naturally as keys.

---

## Mistakes

- **User Mistake:** No specific note provided.
- Forgetting to handle the empty array case.
- Performing two $O(N)$ passes when one pass (updating `max` during counting) is sufficient.
- Confusing "Highest Occurring" with "Majority Element" (Majority requires $> N/2$ occurrences).

---

## Complexity

**Time:** $O(N)$ → We traverse the array exactly once.  
**Space:** $O(N)$ → In the worst case (all unique elements), the HashMap stores $N$ entries.

---

## Tags and Properties
  - #dsa #important #revisit #codinginterview
  - #basics #frequencycounting
  - [[HashMap]] [[Array]] [[Counting]]
  - Revision Date: 2026-04-06

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-08)
- [ ] Day 7 Revision (2026-04-13)
- [ ] Day 15 Revision (2026-04-21)
- [ ] Day 30 Revision (2026-05-06)
