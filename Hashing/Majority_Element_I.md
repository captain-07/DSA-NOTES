---
created: 2026-04-25
revisions:
  - 2026-04-27
  - 2026-05-02
  - 2026-05-10
  - 2026-05-25
---

# Majority Element-I

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Google #Microsoft #Adobe #Apple #GoldmanSachs

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #arrays [[Arrays]], #hashmap [[HashMap]], #sorting [[Sorting]], #mooresvoting [[Boyer-Moore Voting Algorithm]]

## Pattern

Boyer-Moore Voting Algorithm / Frequency Counting

---
## Difficulty

Easy
#easy

---

## ⚡ Key Idea (Core Insight)

The **Majority Element** occurs more than `n/2` times. In any sequence, if we pair up and "cancel out" different elements, the element that remains at the end is the only possible candidate for the majority.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Maintain a `candidate` and a `count`. If `count == 0`, pick current as candidate. If `num == candidate`, `count++`, else `count--`.

---

## Approach

### Brute Force
- Iterate through each element and count its occurrences using another loop.
- **Time Complexity:** $O(n^2)$
- **Space Complexity:** $O(1)$

### Better
- Use a **HashMap** to store frequencies of each element. Return the one with count $> n/2$.
- **Time Complexity:** $O(n)$
- **Space Complexity:** $O(n)$

### Optimal (Boyer-Moore Voting)
1. Initialize `candidate = None` and `count = 0`.
2. Traverse the array:
   - If `count == 0`, set `candidate = current_element`.
   - If `current_element == candidate`, `count += 1`.
   - Else, `count -= 1`.
3. The `candidate` is the majority element (if a majority is guaranteed).

---

## Code (Python)

```python
class Solution:
    def majorityElement(self, nums: list[int]) -> int:
        candidate = None
        count = 0
        
        # Phase 1: Find candidate
        for num in nums:
            if count == 0:
                candidate = num
            
            count += 1 if num == candidate else -1
            
        # Phase 2: Majority is guaranteed by problem constraints
        # Otherwise, verify candidate with another pass
        return candidate
```

---

## Dry Run (Smart Example)

**Input:** `nums = [2, 2, 1, 1, 1, 2, 2]`

| Step | Num | Candidate | Count | Explanation |
| :--- | :--- | :--- | :--- | :--- |
| 1 | 2 | 2 | 1 | Count was 0, set candidate to 2. |
| 2 | 2 | 2 | 2 | Match! Increment count. |
| 3 | 1 | 2 | 1 | Mismatch! Decrement count. |
| 4 | 1 | 2 | 0 | Mismatch! Decrement count. |
| 5 | 1 | 1 | 1 | Count was 0, set candidate to 1. |
| 6 | 2 | 1 | 0 | Mismatch! Decrement count. |
| 7 | 2 | 2 | 1 | Count was 0, set candidate to 2. |

**Result:** 2

---

## Edge Cases

- **Single Element:** `[1]` → Returns 1 correctly (count starts at 0, becomes 1).
- **All Same Elements:** `[2, 2, 2]` → Count keeps incrementing.
- **Alternating Elements:** `[1, 2, 1]` → 1 wins as it's the majority.
- **Minimum Majority:** `[1, 1, 2]` → 1 appears 2 times ($> 3/2$).

---

## Mistakes

- **User Mistake:** No specific note provided.
- **Logic Gap:** Thinking sorting ($O(n \log n)$) is the most optimal solution.
- **Assumptions:** Forgetting that Boyer-Moore only works if a majority ($> n/2$) *actually* exists.
- **Implementation:** Not resetting the candidate when the count hits zero.

---

## Complexity

Time: $O(n)$ → Single pass through the array.  
Space: $O(1)$ → Only two variables (`candidate`, `count`) used regardless of input size.

---

## Similar Problems

- [Majority Element II](https://leetcode.com/problems/majority-element-ii/) - Medium
- [Check If a Number Is Majority Element in a Sorted Array](https://leetcode.com/problems/check-if-a-number-is-majority-element-in-a-sorted-array/) - Easy
- [Most Frequent Even Element](https://leetcode.com/problems/most-frequent-even-element/) - Easy

---

## Tags and Properties
  - #dsa #important #revisit  
  - #arrays #mooresvoting #linearsearch
  - [[Boyer-Moore Voting Algorithm]] [[Arrays]]
  - **Revision Date:** 2026-04-25
  - **Problem Link:** [LeetCode - Majority Element](https://leetcode.com/problems/majority-element/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-27)
- [ ] Day 7 Revision (2026-05-02)
- [ ] Day 15 Revision (2026-05-10)
- [ ] Day 30 Revision (2026-05-25)
