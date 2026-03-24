---
created: 2026-03-24
revisions:
  - 2026-03-26
  - 2026-03-31
  - 2026-04-08
  - 2026-04-23
---

# Two Sum

---

## Pattern

- HashMap / Hashing
- Complement Search

---

## ⚡ Key Idea (Core Insight)

- For every element `x`, calculate its complement `target - x`.
- Use a **HashMap** to store previously seen numbers as keys and their indices as values to achieve $O(1)$ lookup for the complement.

---

## ⚡ Quick Recall (VERY IMPORTANT)

- **Complement Check:** `if target - num in seen: return [seen[target - num], i]`
- Use a single pass to build the map and check for the target simultaneously.

---

## Approach

### Brute Force
- Iterate through all pairs $(i, j)$ using nested loops and check if `nums[i] + nums[j] == target`.
- **Time:** $O(n^2)$

### Optimal
- Initialize an empty hash map `prevMap`.
- Iterate through the array once.
- Calculate `diff = target - n`.
- If `diff` exists in `prevMap`, return indices `[prevMap[diff], current_index]`.
- Otherwise, add the current number and its index to `prevMap`.
- **Time:** $O(n)$

---

## Code (Python)

```python
def twoSum(nums: list[int], target: int) -> list[int]:
    prevMap = {}  # val : index

    for i, n in enumerate(nums):
        diff = target - n
        if diff in prevMap:
            return [prevMap[diff], i]
        prevMap[n] = i
```

---

## Dry Run (Smart Example)

**Input:** `nums = [3, 2, 4], target = 6`

| Step | Variables | Explanation |
| :--- | :--- | :--- |
| 1 | `n=3, i=0, diff=3` | `3` not in `prevMap`. Add `{3: 0}`. |
| 2 | `n=2, i=1, diff=4` | `4` not in `prevMap`. Add `{2: 1}`. |
| 3 | `n=4, i=2, diff=2` | `2` **is** in `prevMap`. Return `[prevMap[2], 2]`. |
| **Result** | `[1, 2]` | Correct: `nums[1] + nums[2] = 2 + 4 = 6`. |

---

## Edge Cases

- **Negative Numbers:** Works naturally with the complement logic (e.g., `[-1, -2], target = -3`).
- **Duplicates:** HashMap stores the *first* index encountered; the current index handles the *second* occurrence.
- **Large Inputs:** Linear time ensures efficiency for $n > 10^4$.
- **Only Two Elements:** Minimal input size is handled correctly in the first two steps.

---

## Mistakes

- **Forgot to use HashMap for O(1) lookups** (User Mistake).
- Using the same element twice (e.g., `target = 6, nums = [3, 2, 4]` returning `[0, 0]`).
- Sorting the array first (loses original indices, only useful if returning values).
- Not checking for existence before inserting current element (can lead to using the same index if `target - n == n`).

---

## Complexity

- **Time:** $O(n)$ → Single pass through the array with $O(1)$ average hash map operations.
- **Space:** $O(n)$ → Worst case stores all $n$ elements in the hash map.

---

## Difficulty

Easy
#easy

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Google #Microsoft #Apple #Adobe #Meta

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [x] High  

- **Concepts:**
  - #hashmap [[HashMap]], #array [[Array]], #hashing [[Hashing]]

- **Tags:**
  - #dsa #important #revisit #twosum #leetcode1  
  - [[Two Sum]] [[Complement Strategy]]

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-03-26)
- [ ] Day 7 Revision (2026-03-31)
- [ ] Day 15 Revision (2026-04-08)
- [ ] Day 30 Revision (2026-04-23)
