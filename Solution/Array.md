**## Leetcode solution - Array**

The most common data structure that used to store and process data. It takes O(1) when accessing the data, and O(n) when deleting and adding data.

### 26. Remove Duplicates from Sorted Array
Question: [leetcode](https://leetcode.com/problems/remove-duplicates-from-sorted-array/description/)

Use two pointer strategy, one pointer is used to find the next unique number and relocated to the position of the previous pointer. 
```python
class Solution(object):
    def removeDuplicates(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        
        count = 0
        for i in range(1, len(nums)):
            if nums[i] != nums[i-1]:
                count += 1
                nums[count] = nums[i]
        return count + 1
```

### 27. Remove Element
Question: [leetcode](https://leetcode.com/problems/remove-element/description/)

Use two pointer, if nums[j] == val, record the position and replace with next nums[i]. 
```python
class Solution(object):
    def removeElement(self, nums, val):
        """
        :type nums: List[int]
        :type val: int
        :rtype: int
        """
        j = 0
        i = 0
        while i < len(nums):
            if nums[i] == val:
                i += 1
            else:
                nums[j] = nums[i]
                i += 1
                j += 1
        return j
```

### 35. Search Insert Position
Question: [leetcode](https://leetcode.com/problems/search-insert-position/description/)

This question is a Binary Search, which has O(log n) time complexity.

```python
class Solution(object):
    def searchInsert(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: int
        """
        left, right = 0, len(nums) - 1

        while left <= right:
            mid = (left + right) // 2
            if nums[mid] == target:
                return mid
            elif nums[mid] > target:
                right = mid - 1
            else:
                left = mid + 1
        return left
```

### 66. Plus One

```python
class Solution(object):
    def plusOne(self, digits):
        """
        :type digits: List[int]
        :rtype: List[int]
        """
        i = len(digits) - 1
        while i >= 0:
            if digits[i] < 9:
                digits[i] += 1
                return digits
            digits[i] = 0
            i -= 1

        # all the inputs are 0 eg. [9,9,9] -> [1,0,0,0]
        return [1] + digits
```

### 