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
