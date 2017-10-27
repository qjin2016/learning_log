---
layout: post
title:  "Learning Log 5"
date:   2017-10-03
categories: C++ Leetcode
image:  /preview.jpg
---
### 690. Employee Importance
https://leetcode.com/problems/employee-importance/description/

```python
"""
# Employee info
class Employee:
    def __init__(self, id, importance, subordinates):
        # It's the unique id of each node.
        # unique id of this employee
        self.id = id
        # the importance value of this employee
        self.importance = importance
        # the id of direct subordinates
        self.subordinates = subordinates
"""
class Solution:
    def getImportance(self, employees, id):
        """
        :type employees: Employee
        :type id: int
        :rtype: int
        """
        emps = {employee.id: employee for employee in employees}
        def dfs(id):
            return sum([dfs(sub_id) for sub_id in emps[id].subordinates]) + emps[id].importance
        return dfs(id)
```


### 684. Redundant Connection
https://leetcode.com/problems/redundant-connection/description/

```python
class UnionFind():
    def __init__(self, n):
        self.set = range(n)
        self.n = n
        
    def find_set(self, x):
        if self.set[x] != x:
            self.set[x] = self.find_set(self.set[x])
        return self.set[x]
    
    def union_set(self, x, y):
        x_root, y_root = map(self.find_set, (x, y))
        if x_root == y_root:
            return False
        self.set[min(x_root, y_root)] = max(x_root, y_root)
        self.n -= 1
        return True



class Solution(object):
    def findRedundantConnection(self, edges):
        """
        :type edges: List[List[int]]
        :rtype: List[int]
        """
        union_find = UnionFind(len(edges)+1)
        for edge in edges:
            if not union_find.union_set(*edge):
                return edge
        return []
```

### 104. Maximum Depth of Binary Tree
https://leetcode.com/problems/maximum-depth-of-binary-tree/description/

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def maxDepth(self, root):
        """
        :type root: TreeNode
        :rtype: int
        """
        def helper(node, h):
            if node:
                return max(helper(node.left, h+1), helper(node.right, h+1))
            else:
                return h
        h = 0
        return helper(root, h)
```


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

  - solution 2 (union find):

```python
class Solution(object):
    def get_root(self, root, i):
        while i != root[i]:
            root[i] = root[root[i]]
            i = root[i]
        return i
        
    def findCircleNum(self, M):
        """
        :type M: List[List[int]]
        :rtype: int
        """
        root = [i for i in range(len(M))]
        n = len(M)
        for i in range(len(M)):
            for j in range(len(M)):
                if M[i][j] == 1:
                    root1 = self.get_root(root, i)
                    root2 = self.get_root(root, j)
                    if root1 != root2:
                        n -= 1
                        root[root2] = root1
        return n
```

- data buffer vs. cache,
  - data buffer and cache are quite similar. Except that cache operates on the premise that the data will be used multiple times. 
  
- str() function in python operates by converting a python object into a string. A list can also be directly converted into a string.





