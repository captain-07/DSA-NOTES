---
created: 2026-04-10
revisions:
  - 2026-04-12
  - 2026-04-17
  - 2026-04-25
  - 2026-05-10
---

# Binary Search

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Google #Amazon #Microsoft #Meta #Apple #Netflix

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #searching [[Searching]], #binary-search [[Binary Search]], #divide-and-conquer [[Divide and Conquer]]

## Pattern

- Binary Search (Sorted Array)

---
## Difficulty

Easy  
#easy

---

## ⚡ Key Idea (Core Insight)

- Exploits the property of **sorted data** to eliminate half of the remaining search space in each iteration.
- By comparing the `target` with the `middle` element, you decide whether to search in the left or right half.

---

## ⚡ Quick Recall (VERY IMPORTANT)

- `while low <= high`: Use `low + (high - low) // 2` to find mid and avoid overflow.
- If `nums[mid] < target`, move `low = mid + 1`.

---

## Approach

### Brute Force
- Linear Search: Iterate through every element in the array until the target is found.
- Time Complexity: O(N)

### Optimal
1. Initialize `low = 0` and `high = len(nums) - 1`.
2. While `low <= high`:
   - Calculate `mid`.
   - If `nums[mid] == target`, return `mid`.
   - If `nums[mid] < target`, discard the left half (`low = mid + 1`).
   - If `nums[mid] > target`, discard the right half (`high = mid - 1`).
3. Return -1 if not found.

---

## Code (Python)

```python
class Solution:
    def search(self, nums: list[int], target: int) -> int:
        low, high = 0, len(nums) - 1
        
        while low <= high:
            # Avoid potential overflow in other languages
            mid = low + (high - low) // 2
            
            if nums[mid] == target:
                return mid
            elif nums[mid] < target:
                low = mid + 1
            else:
                high = mid - 1
                
        return -1
```

---

## Dry Run (Smart Example)

**Input:** `nums = [-1, 0, 3, 5, 9, 12]`, `target = 9`

| Step | Variables | Explanation |
| :--- | :--- | :--- |
| 1 | `low=0, high=5, mid=2` | `nums[2] = 3`. Since `3 < 9`, search right half. |
| 2 | `low=3, high=5, mid=4` | `nums[4] = 9`. Target found! |
| 3 | **Result: 4** | Return index 4. |

---

## Edge Cases

- **Empty Array:** `nums = []` → Loop doesn't run, returns -1.
- **Target at Boundaries:** Target is the first or last element.
- **Array Size 1:** Single element matches or doesn't match target.
- **Target Not Found:** `low` eventually exceeds `high`.

---

## Mistakes

- **Integer Overflow:** Calculating `mid = (low + high) // 2` can overflow in C++/Java (use `low + (high - low) // 2`).
- **Infinite Loop:** Incorrectly updating pointers (e.g., `low = mid` instead of `low = mid + 1`).
- **Loop Condition:** Using `while low < high` instead of `low <= high` (misses the last element).
- **User mistake:** No specific note provided.

---

## Complexity

Time: O(log N) → The search space is halved in every iteration.  
Space: O(1) → Only a constant amount of extra space is used for pointers.

---

## Similar Problems

- [Search in Rotated Sorted Array](https://leetcode.com/problems/search-in-rotated-sorted-array/) - Medium
- [Find First and Last Position of Element in Sorted Array](https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/) - Medium
- [Search Insert Position](https://leetcode.com/problems/search-insert-position/) - Easy
- [Sqrt(x)](https://leetcode.com/problems/sqrtx/) - Easy

---

## Tags and Properties
  - #dsa #important #revisit  
  - #searching #arrays #logarithmic 
  - [[Binary Search]] [[Searching Algorithms]]
  - **Revision Date:** 2026-04-10
  - **Problem Link:** [Binary Search - LeetCode](https://leetcode.com/problems/binary-search/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-12)
- [ ] Day 7 Revision (2026-04-17)
- [ ] Day 15 Revision (2026-04-25)
- [ ] Day 30 Revision (2026-05-10)
