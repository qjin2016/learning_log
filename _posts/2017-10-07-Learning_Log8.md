---
layout: post
title:  "Learning Log 8"
date:   2017-10-07
categories: C++ Python Leetcode
image:  /preview.jpg
---

### 2 Add Two Numbers 
https://leetcode.com/problems/add-two-numbers/solution/

- Solution 1, naive approach:

```python
# Definition for singly-linked list.
class ListNode:
    def __init__(self, x):
        self.val = x
        self.next = None

class Solution:
    def addTwoNumbers(self, l1, l2):
        """
        :type l1: ListNode
        :type l2: ListNode
        :rtype: ListNode
        """
        num1 = ''
        while l1:
            num1 += str(l1.val)
            l1 = l1.next
        num1 = int(num1[::-1])
        
        num2 = ''
        while l2:
            num2 += str(l2.val)
            l2 = l2.next
        num2 = int(num2[::-1])
        
        num = list(str(num1 + num2))
        l = ListNode(int(num.pop()))
        cur = l
        while num:
            cur.next = ListNode(int(num.pop()))
            cur = cur.next
        return l
```

- Solution 2:

```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def addTwoNumbers(self, l1, l2):
        """
        :type l1: ListNode
        :type l2: ListNode
        :rtype: ListNode
        """
        res = ListNode(None)
        head = res
        prev_extra = 0
        while l1 or l2 or prev_extra:
            if l1 and l2:
                summed = l1.val + l2.val
                l1 = l1.next
                l2 = l2.next
            elif l1 is None and l2 is None:
                summed = 0
            elif l1 is None and l2 is not None:
                summed = l2.val
                l2 = l2.next
            else:
                summed = l1.val
                l1 = l1.next
            extra = (summed + prev_extra) % 10
            prev_extra = int((summed + prev_extra) / 10)
            res.next = ListNode(extra)
            res = res.next
        return head.next
```

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
