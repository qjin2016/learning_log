---
layout: post
title:  "Learning Log 10"
date:   2017-10-12
categories: UnionFind Leetcode
image:  /preview.jpg
---

### Disjoint-set data structure 

a disjoint-set data structure supports the following operations:

- MakeSet(x) creates a singleton set {x}
- Find(x) returns ID of the set
- Union(x, y) merges two sets containing x and y

(coursera, https://www.coursera.org/learn/data-structures/lecture/JssSY/overview)

#### leetcode 684, Redundant Connection

(https://leetcode.com/problems/redundant-connection/description/)

```python 
class Solution:
    def get_root(self, root, i):
        while i != root[i]:
            root[i] = root[root[i]]
            i = root[i]
        return i
    
    
    def findRedundantConnection(self, edges):
        """
        :type edges: List[List[int]]
        :rtype: List[int]
        """
        root = [i for i in range(1001)]
        for edge in edges:
            x, y = edge
            root_x = self.get_root(root, x)
            root_y = self.get_root(root, y)
            if root_x != root_y:
                root[min(root_x, root_y)] = max(root_x, root_y)
            else:
                return edge
```

#### 323, Number of Connected Components in an Undirected Graph

(https://leetcode.com/problems/number-of-connected-components-in-an-undirected-graph/description/)

```python
class Solution(object):
        
    def countComponents(self, n, edges):
        def find(x):
            if parent[x] != x:
                parent[x] = find(parent[x])
            return parent[x]
            
        def union(xy):
            x, y = map(find, xy)
            if rank[x] < rank[y]:
                parent[x] = y
            else:
                parent[y] = x
                if rank[x] == rank[y]:
                    rank[x] += 1
        
        parent, rank = range(n), [0] * n
        map(union, edges)
        return len({find(x) for x in parent})
```
