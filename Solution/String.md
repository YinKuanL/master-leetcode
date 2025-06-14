## Leetcode solution - String

 A string is often implemented as an array data structure of bytes (or words) that stores a sequence of elements, typically characters, using some character encoding.
 
### 14. Longest Common Prefix
Question: [Leetcode](https://leetcode.com/problems/longest-common-prefix/)

If we want to find the largest common prefix, we can take the first element in the list and find the largest prefix that exists in all strings. If not, then tailor the prefix.
```python
class Solution(object):
    def longestCommonPrefix(self, strs):
        if not strs:
            return ""
        
        prefix = strs[0]

        for i in strs[1:]:
            while not i.startswith(prefix):
                prefix = prefix[:-1]
                if not prefix:
                    return ""
        return prefix
```

### 28. Find the Index of the First Occurrence in a String

Question: [Leetcode](https://leetcode.com/problems/find-the-index-of-the-first-occurrence-in-a-string/)
```python
class Solution(object):
    def strStr(self, haystack, needle):
        """
        :type haystack: str
        :type needle: str
        :rtype: int
        """
        if needle == "":
            return 0

        if len(needle) > len(haystack):
            return -1
        
        j = 0
        while j <= len(haystack) - len(needle):
            i = 0
            while i < len(needle) and haystack[j + i] == needle[i]:
                i += 1
            if i == len(needle):
                return j
            j += 1
        return -1
```