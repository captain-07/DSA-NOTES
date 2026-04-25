---
created: 2026-04-25
revisions:
  - 2026-04-27
  - 2026-05-02
  - 2026-05-10
  - 2026-05-25
---

# Count Subarrays With Given Xor K

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Google #Microsoft #Ola #OYO

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #hashmap [[HashMap]], #bit-manipulation [[Bit Manipulation]], #prefix-sum [[Prefix Sum]]

## Pattern

Prefix XOR + HashMap (Frequency Map)

---
## Difficulty

Medium  
#medium

---

## ⚡ Key Idea (Core Insight)

The fundamental XOR property: If $A \oplus B = C$, then $A \oplus C = B$.  
Let $XR$ be the XOR of the subarray from index $0$ to $i$. If there exists a prefix with XOR $P$ such that the XOR of the remaining subarray is $K$, then $P \oplus K = XR$, which implies **$P = XR \oplus K$**.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Maintain a running `prefix_xor`. At each step, the number of valid subarrays ending here is the frequency of `(prefix_xor ^ k)` already stored in the HashMap.

---

## Approach

### Brute Force
- Iterate through all possible subarrays using nested loops, calculate XOR for each, and check if it equals $K$.
- **Time Complexity:** $O(N^3)$ or $O(N^2)$ with prefix optimization.

### Better
- Not applicable (The jump from $O(N^2)$ to $O(N)$ is direct using a HashMap).

### Optimal
1. Initialize `xr = 0`, `cnt = 0`, and a HashMap `freq = {0: 1}` (to handle cases where prefix itself is $K$).
2. Traverse the array, update `xr ^= num`.
3. Calculate `target = xr ^ k`.
4. Add `freq[target]` to `cnt`.
5. Update `freq[xr] = freq.get(xr, 0) + 1`.

---

## Code (Python)

```python
class Solution:
    def solve(self, A: list[int], B: int) -> int:
        """
        A: List of integers
        B: Target XOR value (K)
        """
        xr = 0
        # Map to store frequency of prefix XORs
        freq = {0: 1} 
        count = 0
        
        for num in A:
            # Prefix XOR till current index
            xr ^= num
            
            # Target prefix we are looking for: P = xr ^ B
            target = xr ^ B
            
            # If target exists in map, add its frequency to count
            if target in freq:
                count += freq[target]
            
            # Update current prefix XOR frequency in map
            freq[xr] = freq.get(xr, 0) + 1
            
        return count
```

---

## Dry Run (Smart Example)

**Input:** `A = [4, 2, 2, 6, 4], K = 6`

| Step | Num | `xr` (Prefix) | `target` (xr ^ K) | `freq` Map (State after) | `count` | Explanation |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| Start | - | 0 | - | `{0:1}` | 0 | Initial state |
| 1 | 4 | 4 | $4 \oplus 6 = 2$ | `{0:1, 4:1}` | 0 | 2 not in map |
| 2 | 2 | 6 | $6 \oplus 6 = 0$ | `{0:1, 4:1, 6:1}` | 1 | 0 found in map (Subarray `[4,2]`) |
| 3 | 2 | 4 | $4 \oplus 6 = 2$ | `{0:1, 4:2, 6:1}` | 1 | 2 not in map |
| 4 | 6 | 2 | $2 \oplus 6 = 4$ | `{0:1, 4:2, 6:1, 2:1}` | 3 | 4 found twice (Subarrays `[2,2,6]` and `[6]`) |
| 5 | 4 | 6 | $6 \oplus 6 = 0$ | `{0:1, 4:2, 6:2, 2:1}` | 4 | 0 found once (Subarray `[4,2,2,6,4]`) |

---

## Edge Cases

- **K is 0:** Requires counting subarrays where all elements XOR to 0 (duplicates in `xr` will trigger this).
- **All elements same:** e.g., `[2, 2, 2], K = 2`. Correctly handles multiple valid subarrays.
- **No subarray matches K:** `count` remains 0.
- **Single element array:** Works if `A[0] == K`.

---

## Mistakes

- **Forgetting `{0: 1}`:** If the prefix XOR itself equals $K$, you need `0` in the map to count it.
- **Wrong XOR property:** Using `xr ^ target == k` is correct, but mistakenly searching for `xr ^ k` as `target` is the specific derivation.
- **User mistake:** No specific note provided.

---

## Complexity

Time: O(N) → Single pass through the array with $O(1)$ average HashMap lookups.  
Space: O(N) → In worst case (all prefix XORs unique), we store $N$ entries in the HashMap.

---

## Similar Problems

- [Subarray Sum Equals K](https://leetcode.com/problems/subarray-sum-equals-k/) - Medium
- [Subarray Sums Divisible by K](https://leetcode.com/problems/subarray-sums-divisible-by-k/) - Medium
- [Count Subarrays with Fixed Bounds](https://leetcode.com/problems/count-subarrays-with-fixed-bounds/) - Hard
- [Longest Subarray with XOR K](https://www.geeksforgeeks.org/longest-subarray-having-xor-k/) - Medium

---

## Tags and Properties
- #dsa #important #revisit #interview-favorite 
- [[HashMap]] [[Bit Manipulation]] [[Prefix Sum]]
- **Revision Date:** April 25, 2026
- **Problem Link:** [InterviewBit: Subarray with given XOR](https://www.interviewbit.com/problems/subarray-with-given-xor/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-27)
- [ ] Day 7 Revision (2026-05-02)
- [ ] Day 15 Revision (2026-05-10)
- [ ] Day 30 Revision (2026-05-25)
