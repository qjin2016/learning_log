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
