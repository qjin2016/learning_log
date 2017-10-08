---
layout: post
title:  "Learning Log 8"
date:   2017-10-07
categories: C++ Python Leetcode
image:  /preview.jpg
---

- 2 Add Two Numbers (https://leetcode.com/problems/add-two-numbers/solution/)

- 3 Longest Substring Without Repeating Characters (https://leetcode.com/problems/longest-substring-without-repeating-characters/description/)

- 5 Longest Palindromic Substring (https://leetcode.com/problems/longest-palindromic-substring/discuss/)

- 9 Palindrome Number (https://leetcode.com/problems/palindrome-number/description/)

  - Solution 1, convert to string, faster, because the slicing operation is optimized in C

```python
class Solution(object):
    def isPalindrome(self, x):
        """
        :type x: int
        :rtype: bool
        """
        x = str(x)
        return x == x[::-1]
```
  
  - Solution 2

```python
class Solution(object):
    def isPalindrome(self, x):
        """
        :type x: int
        :rtype: bool
        """
        y = 0
        x_copy = x
        while x>0:
            y = y*10+(x%10)
            x = int(x/10)
        return x_copy == y
```
- 
