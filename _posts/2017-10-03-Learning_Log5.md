---
layout: post
title:  "Learning Log 5"
date:   2017-10-03
categories: C++ Leetcode
image:  /preview.jpg
---

### coding:
- 690, Employee Importance (https://leetcode.com/problems/employee-importance/description/)

- 684, Redundant Connection (https://leetcode.com/problems/redundant-connection/description/)

- 126, Word Ladder 2 (https://leetcode.com/problems/word-ladder-ii/description/)

- 547, Friend Circles (https://leetcode.com/problems/friend-circles/description/)

  - solution 1 (DFS):

```python
from collections import deque

class Solution(object):
        
    def findCircleNum(self, M):
        """
        :type M: List[List[int]]
        :rtype: int
        """
        visited = [False for x in range(len(M))]
        
        n = len(M[0])
        
        for i in range(len(M)):
            if visited[i]:
                next
            else:
                visited[i] = True
                q = deque([i])
                while q:
                    person = q.pop()
                    for other in range(len(M[person])):
                        if visited[other] != True and other != person and M[person][other] == 1:
                            visited[other] = True
                            n -= 1
                            q.append(other)
        return n
```



