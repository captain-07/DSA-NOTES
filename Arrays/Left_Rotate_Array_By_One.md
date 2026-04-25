---
created: 2026-04-25
revisions:
  - 2026-04-27
  - 2026-05-02
  - 2026-05-10
  - 2026-05-25
---

# Left Rotate Array By One

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Microsoft #TCS #Infosys #Wipro

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #arrays [[Arrays]]
  - #implementation [[Implementation]]

---
## Pattern

Array Transformation (In-place Shifting)

---
## Difficulty

Easy  
#easy

---

## ⚡ Key Idea (Core Insight)

To rotate an array left by one, the first element must move to the last position. To make room, every other element from index `1` to `n-1` must shift exactly one position to the left (`arr[i-1] = arr[i]`).

---

## ⚡ Quick Recall (VERY IMPORTANT)

Store `arr[0]`, shift the rest left in a single pass, then plug `arr[0]` into `arr[n-1]`.

---

## Approach

### Brute Force
- Create a new array of the same size. Copy `arr[1:]` to the new array and append `arr[0]` at the end.
- **Time:** O(n) | **Space:** O(n)

### Optimal
- **In-place Shifting:** 
  1. Store the first element in a temporary variable.
  2. Iterate from index `1` to `n-1`, moving each element to `i-1`.
  3. Assign the temporary variable to the last index.
- **Time:** O(n) | **Space:** O(1)

---

## Code (Python)

```python
class Solution:
    def rotateLeftByOne(self, nums: list[int]) -> list[int]:
        """
        Rotates the array to the left by one position in-place.
        """
        n = len(nums)
        if n <= 1:
            return nums
        
        # Step 1: Store the first element
        temp = nums[0]
        
        # Step 2: Shift elements to the left
        for i in range(1, n):
            nums[i - 1] = nums[i]
            
        # Step 3: Place temp at the end
        nums[n - 1] = temp
        
        return nums
```

---

## Dry Run (Smart Example)

**Input:** `nums = [10, -2, 5, 10, 7]`

| Step | Variables | Array State | Explanation |
| :--- | :--- | :--- | :--- |
| Init | `temp = 10` | `[10, -2, 5, 10, 7]` | Store `nums[0]` |
| `i=1`| `nums[0] = nums[1]` | `[-2, -2, 5, 10, 7]` | Shift `-2` left |
| `i=2`| `nums[1] = nums[2]` | `[-2, 5, 5, 10, 7]` | Shift `5` left |
| `i=3`| `nums[2] = nums[3]` | `[-2, 5, 10, 10, 7]` | Shift `10` (duplicate) left |
| `i=4`| `nums[3] = nums[4]` | `[-2, 5, 10, 7, 7]` | Shift `7` left |
| End | `nums[4] = temp` | `[-2, 5, 10, 7, 10]` | Place `10` at last index |

---

## Edge Cases

- **Empty Array `[]`:** Return immediately.
- **Single Element `[1]`:** No change needed.
- **Two Elements `[1, 2]`:** Becomes `[2, 1]`.
- **All Identical Elements `[5, 5, 5]`:** No visible change.
- **Array with Negatives:** Handled naturally by shifting logic.

---

## Mistakes

- **Off-by-one Error:** Starting the loop from `0` instead of `1` or ending early.
- **Overwriting First Element:** Forgetting to store `nums[0]` in a `temp` variable before shifting.
- **Returning New List:** Interviewers usually expect in-place modification for this specific problem.
- **User Mistake:** No specific note provided.

---

## Complexity

- **Time:** O(n) → We traverse the array exactly once.
- **Space:** O(1) → Only one extra variable (`temp`) is used regardless of input size.

---

## Similar Problems

- [Rotate Array (k steps)](https://leetcode.com/problems/rotate-array/) - Medium
- [Move Zeroes](https://leetcode.com/problems/move-zeroes/) - Easy
- [Remove Duplicates from Sorted Array](https://leetcode.com/problems/remove-duplicates-from-sorted-array/) - Easy

---

## Tags and Properties
  - #dsa #important #revisit  
  - #arrays #rotation #easy-pick
  - [[Arrays]] [[Cyclic Shift]]
  - **Revision Date:** 2026-04-25
  - **Problem Link:** [GeeksforGeeks - Left Rotate Array by One](https://www.geeksforgeeks.org/batch/striver-atoz-dsa-course/track/striver-atoz-dsa-it-arrays-easy/problem/left-rotate-an-array-by-one)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-27)
- [ ] Day 7 Revision (2026-05-02)
- [ ] Day 15 Revision (2026-05-10)
- [ ] Day 30 Revision (2026-05-25)
