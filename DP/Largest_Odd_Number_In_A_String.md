---
created: 2026-04-27
revisions:
  - 2026-04-29
  - 2026-05-04
  - 2026-05-12
  - 2026-05-27
---

# Largest Odd Number In A String

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Microsoft #Adobe #Google #Facebook

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #string [[String]], #greedy [[Greedy]], #math [[Mathematics]]

## Pattern

Right-to-Left Linear Scan (Suffix-to-Prefix)

---
## Difficulty

Easy  
#easy

---

## ⚡ Key Idea (Core Insight)

The parity of a number (even or odd) is determined **only by its last digit**. To maximize the value of the odd substring, we must keep the longest possible prefix that ends in an odd digit. Searching from **right to left** guarantees we find the largest substring immediately.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Find the **rightmost odd digit**; return the substring from index `0` to that index (inclusive).

---

## Approach

### Brute Force
- Generate all possible substrings, convert them to integers (if possible/small), and check if they are odd. Keep track of the maximum.
- **Time Complexity:** $O(N^2)$ to generate substrings, $O(N)$ for conversion/check = $O(N^3)$.

### Better
- Iterate through all possible end indices from right to left. For each end index, check if the character is odd. If it is, return the substring from the start to that index.
- **Time Complexity:** $O(N)$. (This is essentially the logic used in optimal, but conceptually avoids checking every single substring).

### Optimal
1. Start a pointer at the end of the string (`n-1`).
2. Move leftward until an odd digit (`1, 3, 5, 7, 9`) is encountered.
3. If an odd digit is found at index `i`, the largest odd number is the substring `num[0 : i+1]`.
4. If the loop finishes without finding an odd digit, return an empty string `""`.

---

## Code (Python)

```python
class Solution:
    def largestOddNumber(self, num: str) -> str:
        # Iterate from the end of the string to the beginning
        for i in range(len(num) - 1, -1, -1):
            # Check if the current digit is odd
            if int(num[i]) % 2 != 0:
                # Return the substring from index 0 to i (inclusive)
                return num[:i + 1]
        
        # If no odd digit is found, return an empty string
        return ""
```

---

## Dry Run (Smart Example)

**Input:** `num = "354276"`

| Step | Index (`i`) | Char | Logic | Result |
| :--- | :--- | :--- | :--- | :--- |
| 1 | 5 | '6' | Even, continue | - |
| 2 | 4 | '7' | **Odd found!** | Stop loop |
| 3 | - | - | Slice `num[0:5]` | "35427" |

---

## Edge Cases

- **No odd digits:** `"2468"` → returns `""`.
- **Entire string is odd:** `"1357"` → returns `"1357"`.
- **Only the first digit is odd:** `"3222"` → returns `"3"`.
- **Only the last digit is odd:** `"2223"` → returns `"2223"`.
- **Empty string/Single digit:** `"7"` → `"7"`, `"8"` → `""`.

---

## Mistakes

- **Integer Overflow:** Trying to convert the entire string to an `int` to check parity. Input can be thousands of digits long.
- **Substring Search:** Checking all substrings instead of just the prefixes.
- **Left-to-Right Scan:** Searching from left to right requires extra memory to store the "last seen" odd position.
- **User Mistake:** No specific note provided (ensure this structure is saved for future reference).

---

## Complexity

Time: $O(N)$ → We traverse the string at most once.  
Space: $O(1)$ → Ignoring the space required for the output substring, we only use a constant amount of extra variables.

---

## Similar Problems

- [Largest 3-Same-Digit Number in String](https://leetcode.com/problems/largest-3-same-digit-number-in-string/) - Easy
- [Remove Trailing Zeros From a String](https://leetcode.com/problems/remove-trailing-zeros-from-a-string/) - Easy
- [Consecutive Characters](https://leetcode.com/problems/consecutive-characters/) - Easy

---

## Tags and Properties
- #dsa #important #revisit #strings #greedy
- [[String]] [[Greedy]]
- **Revision Date:** 2026-04-27
- **Problem Link:** [LeetCode - Largest Odd Number In A String](https://leetcode.com/problems/largest-odd-number-in-a-string/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-29)
- [ ] Day 7 Revision (2026-05-04)
- [ ] Day 15 Revision (2026-05-12)
- [ ] Day 30 Revision (2026-05-27)
