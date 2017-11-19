---
layout: post
title:  "LeetCode"
date:   2017-11-16
categories: leetcode
---

### 243. Shortest Word Distance

https://leetcode.com/problems/shortest-word-distance/description/

```python
class Solution(object):
    def shortestDistance(self, words, word1, word2):
        """
        :type words: List[str]
        :type word1: str
        :type word2: str
        :rtype: int
        """
        diff = len(words)
        idx1, idx2 = diff, diff
        for i, word in enumerate(words):
            if word == word1:
                idx1 = i
                diff = min(diff, abs(idx1 - idx2))
            if word == word2:
                idx2 = i
                diff = min(diff, abs(idx1 - idx2))
        return diff
```


### 624. Maximum Distance in Arrays

https://leetcode.com/problems/maximum-distance-in-arrays/discuss/

```python
class Solution(object):
    def maxDistance(self, arrays):
        """
        :type arrays: List[List[int]]
        :rtype: int
        """
        res, curMin, curMax = 0, 10000, -10000
        for a in arrays :
            res = max(res, max(a[-1]-curMin, curMax-a[0]))
            curMin, curMax = min(curMin, a[0]), max(curMax, a[-1])
        return res
```


### 359. Logger Rate Limiter

https://leetcode.com/problems/logger-rate-limiter/discuss/

```python
class Logger(object):

    def __init__(self):
        """
        Initialize your data structure here.
        """
        self.ok = {}
        

    def shouldPrintMessage(self, timestamp, message):
        """
        Returns true if the message should be printed in the given timestamp, otherwise returns false.
        If this method returns false, the message will not be printed.
        The timestamp is in seconds granularity.
        :type timestamp: int
        :type message: str
        :rtype: bool
        """
        if timestamp < self.ok.get(message, 0):
            return False
        self.ok[message] = timestamp + 10
        return True

# Your Logger object will be instantiated and called as such:
# obj = Logger()
# param_1 = obj.shouldPrintMessage(timestamp,message)
```


### 346. Moving Average from Data Stream

https://leetcode.com/problems/moving-average-from-data-stream/discuss/

```python
import collections

class MovingAverage(object):

    def __init__(self, size):
        """
        Initialize your data structure here.
        :type size: int
        """
        self.queue = collections.deque(maxlen=size)
        

    def next(self, val):
        """
        :type val: int
        :rtype: float
        """
        self.queue.append(val)
        return float(sum(self.queue))/len(self.queue)
        


# Your MovingAverage object will be instantiated and called as such:
# obj = MovingAverage(size)
# param_1 = obj.next(val)
```


### 720. Longest Word in Dictionary

https://leetcode.com/problems/longest-word-in-dictionary/discuss/

```python
class Solution(object):
    def longestWord(self, words):
        """
        :type words: List[str]
        :rtype: str
        """
        words, resword, res = sorted(words), '', set()
        for word in words:
            if len(word) == 1 or word[:-1] in res:
                res.add(word)
                resword = word if resword == '' else resword 
                resword = word if len(word) > len(resword) else resword
        return resword
```


### 167. Two Sum II - Input array is sorted

https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/description/

```python
class Solution(object):
    def twoSum(self, numbers, target):
        """
        :type numbers: List[int]
        :type target: int
        :rtype: List[int]
        """
        start, end = 0, len(numbers)-1
        while start < end:
            cur_sum = numbers[start] + numbers[end]
            if cur_sum > target:
                end -= 1
            elif cur_sum < target:
                start += 1
            else:
                return start+1, end+1
```


### 350. Intersection of Two Arrays II

https://leetcode.com/problems/intersection-of-two-arrays-ii/description/

```python
class Solution(object):
    def intersect(self, nums1, nums2):
        """
        :type nums1: List[int]
        :type nums2: List[int]
        :rtype: List[int]
        """
        nums1 = sorted(nums1)
        nums2 = sorted(nums2)
        
        p1, p2 = 0, 0
        commons = []
        while p1 < len(nums1) and p2 < len(nums2):
            if nums1[p1] < nums2[p2]:
                p1 += 1
            elif nums1[p1] > nums2[p2]:
                p2 += 1
            else:
                commons.append(nums1[p1])
                p1 += 1
                p2 += 1
        return commons
```


### 270. Closest Binary Search Tree Value

https://leetcode.com/problems/closest-binary-search-tree-value/description/

```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def closestValue(self, root, target):
        """
        :type root: TreeNode
        :type target: float
        :rtype: int
        """
        path = []
        while root:
            path.append(root.val)
            root = root.left if target < root.val else root.right
        return min(path, key = lambda x: abs(target - x))
```


### 206. Reverse Linked List

https://leetcode.com/problems/reverse-linked-list/description/

#### solution 1
```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def reverseList(self, head):
        """
        :type head: ListNode
        :rtype: ListNode
        """
        stack = []
        while head:
            stack.append(head.val)
            head = head.next
        
        new_head = ListNode(None)
        root = new_head
        for v in stack[::-1]:
            new_head.next = ListNode(v)
            new_head = new_head.next
        return root.next
```

#### solution2
```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def reverseList(self, head):
        """
        :type head: ListNode
        :rtype: ListNode
        """
        prev = None
        while head:
            cur = head
            head = head.next
            cur.next = prev
            prev = cur
        return prev
```


### 141. Linked List Cycle

https://leetcode.com/problems/linked-list-cycle/description/

```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def hasCycle(self, head):
        """
        :type head: ListNode
        :rtype: bool
        """
        if head is None: return False
        walker = head
        runner = head
        while runner.next is not None and runner.next.next is not None:
            walker = walker.next
            runner = runner.next.next
            if walker == runner: return True
        return False
```


### 234. Palindrome Linked List

https://leetcode.com/problems/palindrome-linked-list/description/

```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def isPalindrome(self, head):
        """
        :type head: ListNode
        :rtype: bool
        """
        rev = None
        fast = slow = head
        while fast and fast.next:
            fast = fast.next.next
            rev, rev.next, slow = slow, rev, slow.next
            # slow = slow.next
        slow = slow.next if fast else slow
        while rev and rev.val == slow.val:
            slow = slow.next
            rev = rev.next
        return not rev
```


### 266. Palindrome Permutation

https://leetcode.com/problems/palindrome-permutation/description/

#### Solution1
```python
class Solution(object):
    def canPermutePalindrome(self, s):
        """
        :type s: str
        :rtype: bool
        """
        s = sorted(s)
        arr = []
        for i in s:
            if not arr or i not in arr:
                arr.append(i)
            elif i in arr:
                arr.pop()
        return len(arr) == 1 or len(arr) == 0
```

#### Solution2
```python
class Solution(object):
    def canPermutePalindrome(self, s):
        """
        :type s: str
        :rtype: bool
        """
        return sum(v % 2 for v in collections.Counter(s).values()) < 2
```


### 246. Strobogrammatic Number

https://leetcode.com/problems/strobogrammatic-number/discuss/

```python
class Solution(object):
    def isStrobogrammatic(self, num):
        """
        :type num: str
        :rtype: bool
        """
        return all(num[i] + num[~i] in '696 00 11 88' for i in range(len(num)/2+1))
```


### 170. Two Sum III - Data structure design

https://leetcode.com/problems/two-sum-iii-data-structure-design/discuss/

#### solution1
```python
class TwoSum(object):

    def __init__(self):
        """
        Initialize your data structure here.
        """
        self.nums = []
        

    def add(self, number):
        """
        Add the number to an internal data structure..
        :type number: int
        :rtype: void
        """
        self.nums.append(number)
        

    def find(self, value):
        """
        Find if there exists any pair of numbers which sum is equal to the value.
        :type value: int
        :rtype: bool
        """
        nums = sorted(self.nums)
        if len(nums) < 2: return False
        left, right = 0, len(nums)-1
        while left < right:
            if nums[left] + nums[right] > value:
                right -= 1
            elif nums[left] + nums[right] < value:
                left += 1
            else:
                return True
        return False

# Your TwoSum object will be instantiated and called as such:
# obj = TwoSum()
# obj.add(number)
# param_2 = obj.find(value)
```

#### solution 2
```python
class TwoSum(object):

    def __init__(self):
        """
        Initialize your data structure here.
        """
        self.table = dict()
        

    def add(self, number):
        """
        Add the number to an internal data structure..
        :type number: int
        :rtype: void
        """
        self.table[number] = self.table.get(number, 0) + 1
        

    def find(self, value):
        """
        Find if there exists any pair of numbers which sum is equal to the value.
        :type value: int
        :rtype: bool
        """
        for i in self.table.keys():
            j = value - i
            if i == j and self.table.get(i) > 1 or i != j and self.table.get(j) > 0:
                return True
        return False
        
# Your TwoSum object will be instantiated and called as such:
# obj = TwoSum()
# obj.add(number)
# param_2 = obj.find(value)
```


### 290. Word Pattern

https://leetcode.com/problems/word-pattern/description/

#### solution1
```python
class Solution(object):
    def wordPattern(self, pattern, str):
        """
        :type pattern: str
        :type str: str
        :rtype: bool
        """
        pattern_dict = {}
        str_arr = str.split(' ')
        if len(str_arr) != len(pattern): return False
        
        for p, s in zip(pattern, str_arr):
            if p not in pattern_dict:
                if s in pattern_dict.values():
                    return False
                pattern_dict[p] = s
            else:
                if pattern_dict[p] != s:
                    return False
        return True
```

#### solution2
```python
class Solution(object):
    def wordPattern(self, pattern, str):
        """
        :type pattern: str
        :type str: str
        :rtype: bool
        """
        s = pattern
        t = str.split(' ')
        return map(s.find, s) == map(t.index, t)
```


### 438. Find All Anagrams in a String

https://leetcode.com/problems/find-all-anagrams-in-a-string/discuss/

#### solution 1(too slow...)
```python
class Solution:
    def findAnagrams(self, s, p):
        """
        :type s: str
        :type p: str
        :rtype: List[int]
        """
        from collections import Counter
        win_size = len(p)
        
        set_p = Counter(p)
        idxs = []
        i = 0
        while i + win_size <= len(s):
            if Counter(s[i:i+win_size]) == set_p:
                idxs.append(i)
            i += 1
        return idxs
```

#### solution 2
```python
class Solution:
    def findAnagrams(self, s, p):
        """
        :type s: str
        :type p: str
        :rtype: List[int]
        """
        from collections import Counter
        res = []
        pCounter = Counter(p)
        sCounter = Counter(s[:len(p)-1])
        for i in range(len(p)-1, len(s)):
            sCounter[s[i]] += 1
            if sCounter == pCounter:
                res.append(i-len(p) + 1)
            sCounter[s[i-len(p) + 1]] -= 1
            if sCounter[s[i-len(p) + 1]] == 0:
                del sCounter[s[i-len(p)+1]]
        return res
```


### 500. Keyboard Row

https://leetcode.com/problems/keyboard-row/discuss/

```python
class Solution:
    def findWords(self, words):
        """
        :type words: List[str]
        :rtype: List[str]
        """
        a=set('qwertyuiop')
        b=set('asdfghjkl')
        c=set('zxcvbnm')
        ans=[]
        for word in words:
            t=set(word.lower())
            if a&t==t:
                ans.append(word)
            if b&t==t:
                ans.append(word)
            if c&t==t:
                ans.append(word)
        return ans
```
