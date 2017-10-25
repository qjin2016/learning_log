---
layout: post
title:  "Learning Log 15"
date:   2017-10-25
categories: Leetcode 
image:  /preview.jpg
---

### 692. Top K Frequent Words

https://leetcode.com/problems/top-k-frequent-words/description/

```pyhton
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

