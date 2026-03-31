---
created: 2026-03-31
revisions:
  - 2026-04-02
  - 2026-04-07
  - 2026-04-15
  - 2026-04-30
---

# Binary Search

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Google #Amazon #Microsoft #Meta #Apple #Uber

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #binarysearch [[Binary Search]]
  - #searching [[Searching]]
  - #arrays [[Arrays]]
  - #divideandconquer [[Divide and Conquer]]

---
## Pattern

Search Space Reduction (Divide and Conquer)

---
## Difficulty

Easy
#easy

---

## ⚡ Key Idea (Core Insight)

In a **sorted** range, compare the middle element with the target. Since the data is ordered, you can discard exactly half of the remaining search space in every iteration, reducing the problem size exponentially.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Find `mid`, if `arr[mid] < target`, move `low` to `mid + 1`. Else if `arr[mid] > target`, move `high` to `mid - 1`. Use `low <= high` loop condition.

---

## Approach

### Brute Force
- Linear Search: Iterate through every element one by one until the target is found.
- **Time Complexity:** O(N)

### Optimal
- **Binary Search:**
  1. Initialize `low = 0` and `high = len(arr) - 1`.
  2. While `low <= high`:
     - Calculate `mid = low + (high - low) // 2`.
     - If `arr[mid] == target`, return `mid`.
     - If `arr[mid] < target`, discard left half: `low = mid + 1`.
     - If `arr[mid] > target`, discard right half: `high = mid - 1`.
  3. If loop ends, target is not present.
- **Time Complexity:** O(log N)

---

## Code (Python)

```python
def binary_search(nums: list[int], target: int) -> int:
    low = 0
    high = len(nums) - 1
    
    while low <= high:
        # Calculate mid (prevents integer overflow in other languages)
        mid = low + (high - low) // 2
        
        if nums[mid] == target:
            return mid # Target found
        elif nums[mid] < target:
            low = mid + 1 # Target is in the right half
        else:
            high = mid - 1 # Target is in the left half
            
    return -1 # Target not found
```

---

## Dry Run (Smart Example)

**Input:** `nums = [-5, 0, 3, 5, 9, 12]`, `target = 9`

| Step | low | high | mid | nums[mid] | Explanation |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | 0 | 5 | 2 | 3 | `3 < 9`, set `low = mid + 1 = 3` |
| 2 | 3 | 5 | 4 | 9 | `9 == 9`, return `mid = 4` |

---

## Edge Cases

- **Target at boundaries:** Target is the first or last element.
- **Single element array:** `low`, `high`, and `mid` all point to index 0.
- **Element not present:** Loop terminates with `low > high`.
- **Duplicates:** Standard BS returns *any* index of the target.
- **Empty array:** `low = 0`, `high = -1`, loop never executes.

---

## Mistakes

- **Loop Condition:** Using `low < high` instead of `low <= high` (misses the last element).
- **Mid Calculation:** Using `(low + high) // 2` which can cause overflow in languages like C++/Java (though not Python).
- **Update Logic:** Forgetting to do `mid + 1` or `mid - 1`, leading to infinite loops.
- **Sorted Requirement:** Attempting Binary Search on an unsorted array.
- **User Mistake:** No specific note provided.

---

## Complexity

Time: O(log N) → The search space is halved in each step.  
Space: O(1) → Only a constant amount of extra space is used for pointers.

---

## Tags and Properties
  - #dsa #important #revisit #basics
  - [[Binary Search]] [[Searching Algorithms]]
  - Revision Date: 2026-03-31
  - Related: [[Search in Rotated Sorted Array]], [[First and Last Position of Element]]

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-02)
- [ ] Day 7 Revision (2026-04-07)
- [ ] Day 15 Revision (2026-04-15)
- [ ] Day 30 Revision (2026-04-30)
