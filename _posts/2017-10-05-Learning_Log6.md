---
layout: post
title:  "Learning Log 6"
date:   2017-10-05
categories: C++ Python Leetcode
image:  /preview.jpg
---

### coding:

- 200 Number of Islands

  - Solution 1 (slow)

```python 
from collections import deque

class Solution(object):
    
    def bfs_helper(self, grid, pos):
        for move in [[-1, 0], [0, 1], [1, 0], [0, -1]]:
            n_row = pos[0] + move[0]
            n_col = pos[1] + move[1]
            if 0 <= n_row < len(grid) and 0 <= n_col < len(grid[0]) and grid[n_row][n_col] == '1':
                    yield [n_row, n_col]
        
    
    def numIslands(self, grid):
        """
        :type grid: List[List[str]]
        :rtype: int
        """        
        n = 0
        for i in range(len(grid)):
            for j in range(len(grid[0])):
                if grid[i][j] == '1':
                    n += 1
                    q = deque([[i, j]])
                    while q:
                        cur_pos = q.popleft()
                        print(cur_pos)
                        for next_pos in self.bfs_helper(grid, cur_pos):
                            q.append(next_pos)
            
                            grid[next_pos[0]][next_pos[1]] = '0'
        return n   
```

  - Solution 2
  
```python
class Solution(object):
    def numIslands(self, grid):
        """
        :type grid: List[List[str]]
        :rtype: int
        """
        m = len(grid)
        if m == 0: return 0
        n = len(grid[0])
        
        ans = 0
        for y in range(m):
            for x in range(n):
                if grid[y][x] == '1':
                    ans += 1
                    self.__dfs(grid, x, y, n, m)
        return ans
    
    def __dfs(self, grid, x, y, n, m):
        if x < 0 or x >= n or y < 0 or y >= m or grid[y][x] == '0':
            return
        grid[y][x] = '0'
        self.__dfs(grid, x-1, y, n, m)
        self.__dfs(grid, x+1, y, n, m)
        self.__dfs(grid, x, y-1, n, m)
        self.__dfs(grid, x, y+1, n, m)
        
```

- 292 Nim Game (https://leetcode.com/problems/nim-game/description/)

```python
class Solution(object):
    def canWinNim(self, n):
        """
        :type n: int
        :rtype: bool
        """
        return n%4 != 0
```
