## Leetcode solution - String

 A string is often implemented as an array data structure of bytes (or words) that stores a sequence of elements, typically characters, using some character encoding.
 
### 14. Longest Common Prefix
Question: [leetcode](https://leetcode.com/problems/longest-common-prefix/)

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

Question: [leetcode](https://leetcode.com/problems/find-the-index-of-the-first-occurrence-in-a-string/)
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

### 3. Longest Substring Without Repeating Characters (Medium)

Question: [leetcode](https://leetcode.com/problems/longest-substring-without-repeating-characters/description/)

Generate all possible substrings & check for each substring if it's valid and keep updating maxLen accordingly.
```python
class Solution(object):
    def lengthOfLongestSubstring(self, s):
        """
        :type s: str
        :rtype: int
        """
        MaxLen = 0
        for i in range(0, len(s)):
            index = i
            hashtable = set()
            while index < len(s) and s[index] not in hashtable:
                hashtable.add(s[index])
                index += 1
            MaxLen = max(MaxLen, index - i)
        return MaxLen
```

However, there's a more efficient method to solve the question: Sliding Window, which turns the time complexity O(n^2) into O(n)

```python
class Solution:
    def lengthOfLongestSubstring(self, s):
        char_index = {}
        max_len = 0
        left = 0

        for right in range(len(s)):
            if s[right] in char_index and char_index[s[right]] >= left:
                left = char_index[s[right]] + 1
            char_index[s[right]] = right
            max_len = max(max_len, right - left + 1)

        return max_len

```