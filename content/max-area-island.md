---
title: Max Area of Island 
tags:
  - graph
  - dfs
description: Return the maximum area of an island in grid containing 1's and 0's.
---

## Question
---

You are given a matrix `grid` where `grid[i]` is either a `0` (representing water) or `1` (representing land).

An island is defined as a group of `1`'s connected horizontally or vertically. You may assume all four edges of the grid are surrounded by water.

The **area** of an island is defined as the number of cells within the island.

Return the maximum **area** of an island in `grid`. If no island exists, return `0`.

**Example 1:**

![](https://imagedelivery.net/CLfkmk9Wzy8_9HRyug4EVA/8eeb491c-c8ff-4ed6-78ed-ce4cf87d7200/public)

```java
Input: grid = [
  [0,1,1,0,1],
  [1,0,1,0,1],
  [0,1,1,0,1],
  [0,1,0,0,1]
]

Output: 6
```



Explanation: `1`'s cannot be connected diagonally, so the maximum area of the island is `6`.

**Constraints:**

- `1 <= grid.length, grid[i].length <= 50`



## Solution
---
### Algorithms/Patterns:
- [[DFS on grid]]

### Common Mistakes:


- Make your island_area variable is passed by reference. 
- Integers are immutable in python. 
	- Any changes done inside the function won't be reflected outside.


### Code:
```python

class Solution:

    def dfs(self, grid, i, j):

        if i < 0 or j < 0 or i >= len(grid) or j >= len(grid[0]) or grid[i][j] != 1:
            return 0

        grid[i][j] = 2
        island_area = 1

        island_area += self.dfs(grid, i - 1, j)
        island_area += self.dfs(grid, i + 1, j)
        island_area += self.dfs(grid, i, j - 1)
        island_area += self.dfs(grid, i, j + 1)

        return island_area



    def maxAreaOfIsland(self, grid: List[List[int]]) -> int:

        n = len(grid)
        m = len(grid[0])
        max_area = 0

        for i in range(n):
            for j in range(m):
                if grid[i][j] == 1:
                
                    island_area = self.dfs(grid, i, j)
                    max_area = max(max_area, island_area)

        return max_area
```