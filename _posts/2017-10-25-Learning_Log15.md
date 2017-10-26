---
layout: post
title:  "Learning Log 15"
date:   2017-10-25
categories: Leetcode 
image:  /preview.jpg
---

### 692. Top K Frequent Words

https://leetcode.com/problems/top-k-frequent-words/description/

```python
class Solution(object):
    def topKFrequent(self, words, k):
        """
        :type words: List[str]
        :type k: int
        :rtype: List[str]
        """
        # Time: O(n + klgk)
        # Space: O(n)
        from collections import Counter
        counter = Counter(words)
        freqs = {}
        for word, count in counter.items():
            if count not in freqs:
                freqs[count] = []
            freqs[count].append(word)
        res = []
        for i in range(len(words), 0, -1):
            if i in freqs:
                for word in freqs[i]:
                    res.append((word, i))
            if len(res) >= k:
                break
        res = sorted(res, key=lambda r: [-r[1], r[0]])
        return [el[0] for el in res[:k]]
```

### Trie (Prefix Tree)
### 208. Implement Trie (Prefix Tree)

https://leetcode.com/problems/implement-trie-prefix-tree/description/

```python
class TrieNode:
    def __init__(self):
        self.word = False
        self.children = {}

class Trie:
    def __init__(self):
        self.root = TrieNode()
        
    def insert(self, word):
        node = self.root
        for i in word:
            if i not in node.children:
                node.children[i] = TrieNode()
            node = node.children[i]
        node.word = True
        
    def search(self, word):
        node = self.root
        for i in word:
            if i not in node.children:
                return False
            node = node.children[i]
        return node.word
    
    def startsWith(self, prefix):
        node = self.root
        for i in prefix:
            if i not in node.children:
                return False
            node = node.children[i]
        return True
```

128. Longest Consecutive Sequence

https://leetcode.com/problems/longest-consecutive-sequence/description/

```python
class Solution(object):
    def longestConsecutive(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        nums = set(nums)
        best = 0
        for x in nums:
            if x - 1 not in nums:
                y = x + 1
                while y in nums:
                    y += 1
                best = max(best, y - x)
        return best
```
