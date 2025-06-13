## Leetcode solution - Dynamic Programming
Dynamic programming (DP) is a technique for solving optimization problems by breaking them down into smaller, overlapping subproblems and storing their solutions to avoid redundant calculations.
Typically, DP includes three different parts:
1. Recursion
2. Store (Memoize) * not Memorize
3. Bottom-up

### 70. Climbing Stairs
Question: [leetcode](https://leetcode.com/problems/climbing-stairs/description/)

This question is similar to fibonacci sequence, where when i=1 steps=1, i=2 steps=2, i=3 steps=3, i=4 steps=5, and so on.
Therefore, here, we use Dynamic Programming which has O(n) time complexity.

```python
class Solution(object):
    def climbStairs(self, n):
        """
        :type n: int
        :rtype: int
        """

        if n == 1:
            return 1
        if n == 2:
            return 2 # 1+1 or 2
        steps = [0, 1, 2]
        for i in range(3, n+1):
            steps.append(steps[i-1] + steps[i-2])
        return steps[n]
```

### 118. Pascal's Triangle
Question: [leetcode](https://leetcode.com/problems/pascals-triangle/description/)

```python
class Solution(object):
    def generate(self, numRows):
        """
        :type numRows: int
        :rtype: List[List[int]]
        """
        output = []
        for i in range(numRows):
            if i == 0:
                output.append([1])
            else:
                prev = output[-1]
                row = [1] + [prev[j] + prev[j - 1] for j in range(1, i)] + [1]
                output.append(row)
        return output
```