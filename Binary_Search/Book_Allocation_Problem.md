---
created: 2026-04-18
revisions:
  - 2026-04-20
  - 2026-04-25
  - 2026-05-03
  - 2026-05-18
---

# Book Allocation Problem

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Google #Amazon #Microsoft #Flipkart #Adobe

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #binarysearch [[Binary Search]]
  - #greedy [[Greedy]]
  - #arrays [[Arrays]]

## Pattern

Binary Search on Answer (Monotonic Search Space)

---
## Difficulty

Hard
#hard

---

## ⚡ Key Idea (Core Insight)

The answer (maximum pages assigned to a student) must lie between `max(arr)` (at least one student must take the largest book) and `sum(arr)` (one student takes all books). Since this range is sorted, use **Binary Search** to find the minimum value that satisfies the constraint of `M` students.

---

## ⚡ Quick Recall (VERY IMPORTANT)

If `countStudents(pages) > M`, the limit is too **low** (need more pages per student) → `low = mid + 1`. Otherwise, the limit is **feasible**, try for a smaller maximum → `high = mid - 1`.

---

## Approach

### Brute Force
- Check every possible integer from `max(arr)` to `sum(arr)` linearly.
- Time Complexity: O(N * (Sum - Max))

### Optimal (Binary Search on Answer)
1. Define search space: `low = max(arr)`, `high = sum(arr)`.
2. While `low <= high`:
   - Calculate `mid` (candidate for minimum maximum pages).
   - Use a greedy helper function `isPossible(mid)` to check if books can be assigned to `M` students without any student exceeding `mid` pages.
   - If `isPossible`: Store `mid` as answer and try smaller (`high = mid - 1`).
   - If NOT `isPossible`: Try larger (`low = mid + 1`).
3. Return `low`.

---

## Code (Python)

```python
class Solution:
    def findPages(self, arr: list[int], n: int, m: int) -> int:
        # Edge Case: More students than books
        if m > n:
            return -1
        
        def count_students(max_pages_allowed: int) -> int:
            students = 1
            current_pages = 0
            for pages in arr:
                if current_pages + pages <= max_pages_allowed:
                    # Can add to current student
                    current_pages += pages
                else:
                    # Assign to next student
                    students += 1
                    current_pages = pages
            return students

        low = max(arr)
        high = sum(arr)
        ans = low
        
        while low <= high:
            mid = (low + high) // 2
            # If students required is <= available students, mid is feasible
            if count_students(mid) <= m:
                ans = mid
                high = mid - 1
            else:
                # mid is too small, need to increase limit
                low = mid + 1
                
        return low
```

---

## Dry Run (Smart Example)

Input: `arr = [12, 34, 67, 90]`, `m = 2` | `low=90, high=203`

| Step | Mid | Student Count Logic | Result | Action |
| :--- | :--- | :--- | :--- | :--- |
| 1 | 146 | [12+34+67], [90] | 2 students | Feasible: `high = 145`, `ans = 146` |
| 2 | 117 | [12+34+67], [90] | 2 students | Feasible: `high = 116`, `ans = 117` |
| 3 | 103 | [12+34], [67], [90] | 3 students | Too small (3 > 2): `low = 104` |
| 4 | 110 | [12+34], [67], [90] | 3 students | Too small (3 > 2): `low = 111` |
| 5 | 113 | [12+34], [67], [90] | 3 students | Too small (3 > 2): `low = 114` |

Final Answer: **113** (Loop ends, `low` becomes 113)

---

## Edge Cases

- `m > n`: Return -1 (not enough books for each student to have at least one).
- `m == 1`: Return `sum(arr)` (one student takes everything).
- `m == n`: Return `max(arr)` (each student takes one book).
- All books have equal pages: Standard binary search logic applies.

---

## Mistakes

- **Comparison Confusion:** In `isPossible`, if `current_sum + pages > mid`, you MUST start a new student. 
- **Binary Search logic:** If `students_needed > M`, it means `mid` is too **small** (greater than comparison).
- **Initialization:** `low` must start at `max(arr)`, not `0` or `1`, because a student must be able to carry at least the largest single book.
- **Returning the wrong value:** Ensure you return `low` or the stored `ans` after the loop.

---

## Complexity

Time: O(N * log(Sum - Max)) → Binary search takes `log(range)` steps, each step iterates through `N` books.  
Space: O(1) → Only a few variables used for tracking sums and counts.

---

## Similar Problems

- [Split Array Largest Sum](https://leetcode.com/problems/split-array-largest-sum/) - Hard
- [Capacity To Ship Packages Within D Days](https://leetcode.com/problems/capacity-to-ship-packages-within-d-days/) - Medium
- [Koko Eating Bananas](https://leetcode.com/problems/koko-eating-bananas/) - Medium
- [Aggressive Cows](https://www.geeksforgeeks.org/problems/aggressive-cows/1) - Medium

---

## Tags and Properties
  - #dsa #important #revisit  
  - #binarysearch #greedy #interview-classic
  - [[Binary Search]] [[Greedy Algorithms]]
  - **Problem Link:** [GeeksforGeeks - Allocate Minimum Pages](https://www.geeksforgeeks.org/problems/allocate-minimum-number-of-pages0937/1)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-20)
- [ ] Day 7 Revision (2026-04-25)
- [ ] Day 15 Revision (2026-05-03)
- [ ] Day 30 Revision (2026-05-18)
