---
created: 2026-08-08
revisions:
  - 2026-08-10
  - 2026-08-15
  - 2026-08-23
  - 2026-09-07
---

# Asteroid Collision

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Google #Microsoft #Netflix

- **Confidence Checklist:**
  - [ ] Low
  - [ ] Medium
  - [ ] High

- **Concepts:**
  - #stack [[Stack]], #simulation [[Simulation]]

## Pattern

Stack-based Collision Simulation

---
## Difficulty

Medium
#medium

---

## ⚡ Key Idea (Core Insight)

- Collision occurs only when a right-moving asteroid (`+`) meets a left-moving asteroid (`-`) to its right.
- Use a stack to simulate collisions in a single pass.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Process left-to-right: push right-moving asteroids; for left-moving ones, pop smaller right-moving ones until collision, mutual destruction, or path is clear.

---

## Approach

### Brute Force
- Repeatedly scan the array for adjacent colliding pairs (`+` followed by `-`), remove or update them, and repeat.
- Time Complexity: O(N^2)

### Better
- N/A (A single pass stack simulation is optimal)

### Optimal
- Iterate through each asteroid.
- If it moves right (`> 0`), push to the stack.
- If it moves left (`< 0`):
  - While stack has a right-moving asteroid (`> 0`) smaller than the absolute value of the current: pop the stack.
  - If stack top matches the current absolute value: pop stack and destroy current (do not push).
  - If stack top is larger: current is destroyed.
  - If no right-moving asteroid remains on stack top: push current.

---

## Code (Python)

```python
class Solution:
    def asteroidCollision(self, asteroids: list[int]) -> list[int]:
        stack = []
        for ast in asteroids:
            # Process collision only when stack top is positive and current is negative
            while stack and ast < 0 < stack[-1]:
                if stack[-1] < -ast:
                    stack.pop() # Top asteroid is destroyed; continue check
                    continue
                elif stack[-1] == -ast:
                    stack.pop() # Both are destroyed
                break # Current asteroid is destroyed or both were destroyed
            else:
                stack.append(ast) # No collision occurs, push to stack
        return stack
```

---

## Dry Run (Smart Example)

Input: `[10, 2, -5]`

| Step | Variables | Explanation |
| :--- | :--- | :--- |
| 1 | `ast = 10`, `stack = [10]` | Positive asteroid, pushed to stack. |
| 2 | `ast = 2`, `stack = [10, 2]` | Positive asteroid, pushed to stack. |
| 3 | `ast = -5`, `stack = [10, 2]` | Negative asteroid. Collides with `2`. Since `2 < 5`, `2` is popped. |
| 4 | `ast = -5`, `stack = [10]` | Collides with `10`. Since `10 > 5`, `-5` is destroyed. Loop breaks. |
| End | `stack = [10]` | Loop finishes. Return final stack. |

---

## Edge Cases

- All moving same direction (e.g., `[-2, -5]`): No collisions, stack remains unchanged.
- Negatives before positives (e.g., `[-2, 2]`): They move away from each other, no collision.
- Equal sized collisions (e.g., `[5, -5]`): Both explode, stack becomes empty.
- Multi-collision destruction (e.g., `[8, 2, -8]`): `-8` destroys `2`, then destroys `8` (both pop).

---

## Mistakes

- Incorrectly colliding left-moving asteroids (`-`) on the left with right-moving (`+`) on the right.
- Forgetting to handle the equal magnitude case where both asteroids destroy each other.
- **User Mistake:** No specific note provided.

---

## Complexity

Time: O(N) → Each asteroid is pushed and popped from the stack at most once.
Space: O(N) → Worst-case stack stores all N asteroids.

---

## Similar Problems

- [Daily Temperatures](https://leetcode.com/problems/daily-temperatures/) - Medium
- [Backspace String Compare](https://leetcode.com/problems/backspace-string-compare/) - Easy
- [Remove All Adjacent Duplicates in String II](https://leetcode.com/problems/remove-all-adjacent-duplicates-in-string-ii/) - Medium

---

## Tags and Properties
- #dsa #important #revisit
- #stack [[Stack]] #simulation [[Simulation]] #array [[Array]]
- Revision Date: 2026-08-08
- **Problem Link:** [LeetCode - Asteroid Collision](https://leetcode.com/problems/asteroid-collision/)

---

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-08-10)
- [ ] Day 7 Revision (2026-08-15)
- [ ] Day 15 Revision (2026-08-23)
- [ ] Day 30 Revision (2026-09-07)
