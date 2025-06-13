## Leetcode solution - Hash Table

Hash table has O(n) space complexity when storing data, and has O(1) time complexity when solving the question. 

### 1.Two Sum (Easy)
Question: [leetcode](https://leetcode.com/problems/two-sum/)

Using the hash table to store the projection of the elements and indexes. When searching num[i], determine whether complement (target - num[i]) exists. If true, it means that the complement and num[i] are the two numbers that we need to find. The time complexity of this method is O(n), and the space complexity is O(n) as well.


```python
class Solution:
    def twoSum(self, nums, target):
        hashmap = {}
        for i, v in enumerate(nums):
            complement = target - v
            if complement in hashmap:
                return [hashmap[complement], i]
            hashmap[v] = i
        return []
        #Time complexity: O(n)
        #Space complexity: O(n)
```

### 13. Roman to Integer (Easy)
Question: [leetcode](https://leetcode.com/problems/roman-to-integer/)

```python
class Solution(object):
    def romanToInt(self, s):
        S = []
        for n in range(len(s)):
            S.append(s[n])

        roman = {'I': 1, 'V': 5, 'X': 10, 'L': 50, 'C':100, 'D': 500, 'M': 1000}

        results = []
        for i in S:
            results.append(roman[i])
        for j in range(len(results) - 1):
            if results[j] < results[j+1]:
                results[j] = -1*results[j]
        return sum(results)
```

### 141. Linked List Cycle (Easy)
Question: [leetcode](https://leetcode.com/problems/linked-list-cycle/)

Choosing a set to store the visited nodes, and use in to determine whether the node is visited, which time complexity is O(n) and the space complexity is O(n).
```python
class Solution(object):
    def hasCycle(self, head):
        visited = set()

        while head:
            visited.add(head)
            head = head.next
            if head in visited:
                return True
        return False
```

However, there is a faster method: [Tortoise and Hare Algorithm | Floyd Cycle Detection Algorithm](https://youtu.be/S5TcPmTl6ww?si=_MOhPnjYWVlcekuF)
There are two pointers: slow, which moves one step; and fast, which moves two steps. If slow and fast move to the same point, we can say that there exists a cycle in this linked list; otherwise, when fast reaches None, the statement fails. 
```python
class Solution(object):
    def hasCycle(self, head):
        slow = head 
        fast = head
        while fast and fast.next:
            slow = slow.next
            fast = fast.next.next
            if fast == slow:
                return True
        return False
```
Overall, the time complexity is O(n) and the space complexity is O(1).

### 160. Intersection of Two Linked Lists
Question: [leetcode](https://leetcode.com/problems/intersection-of-two-linked-lists/)

Use two pointer strategy.
```python
class Solution(object):
    def getIntersectionNode(self, headA, headB):
        """
        :type head1, head1: ListNode
        :rtype: ListNode
        """
        if not headA or not headB:
            return None

        pA, pB = headA, headB

        while pA != pB:
            pA = pA.next if pA else headB
            pB = pB.next if pB else headA

        return pA
```

### 169. Majority Element
Question: [leetcode](https://leetcode.com/problems/majority-element/)

If we solve the question using set, and count the sum of appearance, it takes up O(n) space complexity. Therefore, we introduce a new algorithm: Boyer–Moore Voting Algorithm, which takes O(n) time complexity and O(1) space complexity.

```python
class Solution(object):
    def majorityElement(self, nums):
        count = 1
        can = nums[0]
        for i in nums[1:]:
            if count == 0:
                count = 1
                can = i
            elif can == i:
                count += 1
            else:
                count -= 1
        return can
```