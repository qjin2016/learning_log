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

### 3 Longest Substring Without Repeating Characters 
https://leetcode.com/problems/longest-substring-without-repeating-characters/description/

```python
class Solution:
    # @return an integer
    def lengthOfLongestSubstring(self, s):
        start = maxLength = 0
        usedChar = {}
        
        for i in range(len(s)):
            if s[i] in usedChar and start <= usedChar[s[i]]:
                start = usedChar[s[i]] + 1
            else:
                maxLength = max(maxLength, i - start + 1)

            usedChar[s[i]] = i

        return maxLength
```

### 5 Longest Palindromic Substring 
https://leetcode.com/problems/longest-palindromic-substring/discuss/

```python
class Solution:
    # @return a string
    def longestPalindrome(self, s):
        if len(s)==0:
        	return 0
        maxLen=1
        start=0
        for i in xrange(len(s)):
        	if i-maxLen >=1 and s[i-maxLen-1:i+1]==s[i-maxLen-1:i+1][::-1]:
        		start=i-maxLen-1
        		maxLen+=2
        		continue

        	if i-maxLen >=0 and s[i-maxLen:i+1]==s[i-maxLen:i+1][::-1]:
        		start=i-maxLen
        		maxLen+=1
        return s[start:start+maxLen]
```

### 9 Palindrome Number
https://leetcode.com/problems/palindrome-number/description/

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

### 342. Power of Four
https://leetcode.com/problems/power-of-four/description/

```python
class Solution:
    def isPowerOfFour(self, num):
        """
        :type num: int
        :rtype: bool
        """
        while num > 1 or num < -1:
            if num % 4 != 0:
                return False
            num = num / 4
        return True if num == 1 else False
```

### 289. Game of Life
https://leetcode.com/problems/game-of-life/discuss/

```C++
class Solution {
public:
    void gameOfLife(vector<vector<int>>& board) {
        int m = board.size(), n = m ? board[0].size() : 0;
        for (int i=0; i<m; ++i) {
            for (int j=0; j<n; ++j) {
                int count = 0;
                for (int I=max(i-1, 0); I<min(i+2, m); ++I)
                    for (int J=max(j-1, 0); J<min(j+2, n); ++J)
                        count += board[I][J] & 1;
                if (count == 3 || count - board[i][j] == 3)
                    board[i][j] |= 2;
            }
        }
        for (int i=0; i<m; ++i)
            for (int j=0; j<n; ++j)
                board[i][j] >>= 1;
        
    }
};
```

