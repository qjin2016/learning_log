---
layout: post
title:  "Learning Log 16"
date:   2017-10-26
categories: Leetcode 
image:  /preview.jpg
---

### Union-Find

```python
# a naive implementation
from collections import defaultdict

class Graph:
    def __init__(self, num_vertices):
        self.V = num_vertices
        self.graph = defaultdict(list)
        
    def addEdge(self, u, v):
        self.graph[u].append(v)
        
    def find_parent(self, parent, i):
        if parent[i] == -1:
            return i
        if parent[i] != -1:
            return self.find_parent(parent, parent[i])
        
    def union(self, parent, x, y):
        x_set = self.find_parent(parent, x)
        y_set = self.find_parent(parent, y)
        parent[x_set] = y_set
        
    def isCyclic(self):
        parent = [-1 for i in range(self.V)]
        for i in self.graph:
            for j in self.graph[i]:
                x = self.find_parent(parent, i)
                y = self.find_parent(parent, j)
                if x == y:
                    return True
                self.union(parent, x, y)

# testing
g = Graph(3)
g.addEdge(0, 1)
g.addEdge(1, 2)
g.addEdge(2, 0)

g.isCyclic()

# ref: http://www.geeksforgeeks.org/union-find/
```

### Beam Search 
similar to BFS, with predetermined number of nodes for expansion in the next level.








