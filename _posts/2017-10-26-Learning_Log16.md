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

### Tokenization
Given a character sequence, tokenization is the process of chopping it into tokens (words/terms). During tokenization process, punctuation might be discarded. An naive way to tokenize a sentence is to chop on whitespace and throw away punctuation characters.

### NER, Named Entity Recognition
https://www.youtube.com/watch?v=M1BpelGGeMk
Stanford NER toolkit is based upon conditional random field + carefully engineered features
The goal of NER is to pick up named entities (organization, name, date) from text.

ML sequence model for NER:

- IO encoding, binary encoding (a certain named entity exists or not), Stanford NER uses IO encoding;
- BIO encoding, this further divides IO encoding into begin-of-entity or continuation-of-entity.

Max Entropy Markov Model (MEMM) a.k.a. Conditional Markov Model (CMM):

The classifer makes a single decision at a time, conditioned on evidence from observations and previous decisions.

### An intro to CRF by Daphne: 
https://www.youtube.com/watch?v=2BXoj778YU8
used for image segmentation and NLP POS task, where features are highly correlated with each other.

### 293. Flip Game

https://leetcode.com/problems/flip-game/description/

```python
class Solution:
    def generatePossibleNextMoves(self, s):
        """
        :type s: str
        :rtype: List[str]
        """
        if len(s) in [0, 1]: return []
        res = []
        for i in range(0, len(s)-1):
            if s[i] == s[i+1] == '+':
                res.append(s[:i]+'--'+s[i+2:])
        return res
```


