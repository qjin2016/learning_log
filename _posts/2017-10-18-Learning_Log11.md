---
layout: post
title:  "Learning Log 11"
date:   2017-10-18 
categories: Leetcode
image:  /preview.jpg
---

1, Intersection of Two Arrays

https://leetcode.com/problems/intersection-of-two-arrays/description/

```python
class Solution(object):
    def intersection(self, nums1, nums2):
        """
        :type nums1: List[int]
        :type nums2: List[int]
        :rtype: List[int]
        """
        nums1.sort()
        nums2.sort()
        if nums1 is None or nums2 is None:
            return []
        i, j = 0, 0
        intersection = set()
        while i < len(nums1) and j < len(nums2):
            if nums1[i] == nums2[j]:
                intersection.add(nums1[i])
                i += 1
                j += 1
            elif nums1[i] < nums2[j]:
                i += 1
            elif nums1[i] > nums2[j]:
                j += 1
        return list(intersection)
```

44, Wildcard Matching 

https://leetcode.com/problems/wildcard-matching/description/

```python
class Solution(object):
    def isMatch(self, s, p):
        """
        :type s: str
        :type p: str
        :rtype: bool
        """
        # be noted: p is the string that contain '?' or '*'     
        
        i, j = 0, 0
        star = None
        
        while i < len(s):
                
            if j < len(p) and (s[i] == p[j] or p[j] == '?'):
                i += 1
                j += 1
                continue
            if j < len(p) and p[j] == '*':
                star = j
                j += 1
                ss = i
                continue
            if star is not None:
                j = star + 1
                i = ss+1
                ss += 1
                continue
            return False    
        
        while j < len(p) and p[j] == '*': j += 1
                
        return j == len(p)
```
