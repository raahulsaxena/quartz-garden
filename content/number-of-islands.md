---
title: Number of Islands
tags:
  - graph
  - dfs
description: Given a 2D grid, return the number of islands.
---

Given a 2D grid `grid` where `'1'` represents land and `'0'` represents water, count and return the number of islands.

An **island** is formed by connecting adjacent lands horizontally or vertically and is surrounded by water. You may assume water is surrounding the grid (i.e., all the edges are water).

**Example 1:**

```java
Input: grid = [
    ["0","1","1","1","0"],
    ["0","1","0","1","0"],
    ["1","1","0","0","0"],
    ["0","0","0","0","0"]
  ]
Output: 1
```

Copy

**Example 2:**

```java
Input: grid = [
    ["1","1","0","0","1"],
    ["1","1","0","0","1"],
    ["0","0","1","0","0"],
    ["0","0","0","1","1"]
  ]
Output: 4
```

Copy

**Constraints:**

- `1 <= grid.length, grid[i].length <= 100`
- `grid[i][j]` is `'0'` or `'1'`.

## Solution:

### Algorithms/Patterns
- [[DFS on grid]]
### Frequent mistakes
- Each character in the grid is a character, and not a number.
- Make sure to check the boundary conditions while writing the dfs function.


```python

class Solution:

    def dfs(self, grid, i, j):

        if i < 0 or j < 0 or i >= len(grid) or j >= len(grid[0]):
            return

        if grid[i][j] == '2' or grid[i][j] == '0':
            return
            
        grid[i][j] = '2'
        self.dfs(grid, i + 1, j)
        self.dfs(grid, i - 1, j)
        self.dfs(grid, i, j + 1)
        self.dfs(grid, i, j - 1)

        return


    def numIslands(self, grid: List[List[str]]) -> int:

        n = len(grid)
        m = len(grid[0])

        island_count = 0


        for i in range(n):
            for j in range(m):

                if grid[i][j] == '1':

                    self.dfs(grid, i, j)
                    island_count += 1

        return island_count
        
```