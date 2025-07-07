---
title: Rotten Oranges
tags:
  - graph
  - bfs
  - simple-bfs
  - dsa
---


You are given a 2-D matrix `grid`. Each cell can have one of three possible values:

- `0` representing an empty cell
- `1` representing a fresh fruit
- `2` representing a rotten fruit

Every minute, if a fresh fruit is horizontally or vertically adjacent to a rotten fruit, then the fresh fruit also becomes rotten.

Return the minimum number of minutes that must elapse until there are zero fresh fruits remaining. If this state is impossible within the grid, return `-1`.

**Example 1:**

![](https://imagedelivery.net/CLfkmk9Wzy8_9HRyug4EVA/5daa219c-ae90-4027-41c3-6ea4d9158300/public)

```java
Input: grid = [[1,1,0],[0,1,1],[0,1,2]]

Output: 4
```

**Example 2:**

```java
Input: grid = [[1,0,1],[0,2,0],[1,0,1]]

Output: -1
```

**Constraints:**

- `1 <= grid.length, grid[i].length <= 10`


## Solution Approach
---
[[Graph Problems]]
- **Problem insight:**
    
    - A rotten orange spreads rot to adjacent fresh oranges in 1 minute.
    - Multiple rotten oranges rot neighbors simultaneously → Use **multi-source BFS** (start BFS from all rotten oranges).
    
- **Initialize tracking variables:**
    
    - minutes = 0: track time taken for rot to spread level-by-level.
    - freshOranges = 0: to know if we successfully rotted all.
    - queue: to process multiple rotten oranges at once.
    - dirs: for 4-directional adjacency.
    
- **Preprocessing step (Decision #1):**
    
    - Push all `grid[i][j] `== 2 (rotten) to the queue → these are your BFS sources.
    - Count all `grid[i][j]` == 1 (fresh) → you’ll use this at the end to check success.
    
- **BFS processing loop:**
    
    - Process the grid **level-by-level**, where each level = 1 minute.
    - For each level, get level_size = `q.size()` to know how many nodes to process now.
    
- **Decision #2 — Why a boolean flag?**
    
    - minutes++ should only happen **if any fresh orange was rotted in the current level**.
    - **Why?** If no new orange rotted this minute, then rot didn’t spread — don’t count time.
    - So: introduce bool increment_minutes = false; at each level.
    
- **Within each level:**
    
    - For each cell, explore its 4 neighbors.
    - If a neighbor is fresh:
        - Turn it rotten.
        - Add it to queue (to process in next minute).
        - Decrement freshOranges.
        - Set increment_minutes = true to indicate change happened this level.
    
- **After each level (Decision #3):**
    
    - If increment_minutes == true, increment minutes++.
    - If false → this level didn’t rot anything, so don’t count it to avoid off-by-one error.
    
- **Final decision:**
    
    - After BFS ends, check freshOranges.
        - If 0 → return minutes.
        - Else → return -1 (some oranges couldn’t be reached).



### Code: (Python)
```python

class Solution:
    def orangesRotting(self, grid: List[List[int]]) -> int:

        # Multi source BFS
        minutes = 0
        freshOranges = 0
        increment_minutes = False

        dirs = [(-1, 0), (1, 0), (0, 1), (0, -1)]
        m, n = len(grid), len(grid[0])

        q = deque()

        for i in range(m):
            for j in range(n):
                if grid[i][j] == 2:
                    q.append((i, j))

                elif grid[i][j] == 1:
                    freshOranges += 1

        while q:

            level_size = len(q)

            increment_minutes = False

            for i in range(level_size):

                x, y = q.popleft()

                for dx, dy in dirs:

                    nx = x + dx
                    ny = y + dy

                    if nx >= 0 and ny >= 0 and nx < m and ny < n and grid[nx][ny] == 1:

                        grid[nx][ny] = 2
                        freshOranges -= 1
                        q.append((nx, ny))
                        increment_minutes = True

            if increment_minutes:
                minutes += 1

        
        return minutes if freshOranges == 0 else -1

```
### Code: (C++)

```cpp

class Solution {
public:
    int orangesRotting(vector<vector<int>>& grid) {

        // Multi-source BFS

        // Add all the rotten fruits to the queue, then keep visiting the neighbors, marking them visited, and incrementing the time

        int minutes = 0, freshOranges = 0;
        bool increment_minutes = false;

        queue<pair<int, int>> q;

        vector<pair<int, int>> dirs = {{-1, 0}, {1, 0}, {0, 1}, {0, -1}};

        int m = grid.size(), n = grid[0].size();

        for(int i = 0; i < m; i++){
            for(int j = 0; j < n; j++){
                if (grid[i][j] == 2){
                    q.push({i, j});
                }
                else if(grid[i][j] == 1) freshOranges++;
            }
        }

        while(!q.empty()){

            int level_size = q.size();

            increment_minutes = false;

            for(int i = 0; i < level_size; i++){

                auto [x, y] = q.front();
                q.pop();

                // rotten orange

                // make neighbors rot

                for(auto [dx, dy]: dirs){

                    int nx = x + dx, ny = y + dy;

                    if (nx >= 0 && ny >= 0 && nx < m && ny < n && grid[nx][ny] == 1){
                        grid[nx][ny] = 2;
                        freshOranges--;
                        q.push({nx, ny});
                        increment_minutes = true;
                    } 

                }


            }

            // Make sure you don't increment minutes for the last level when all oranges have been rotten - to avoid off by one error
            if(increment_minutes) minutes++;


        }



        return (freshOranges == 0) ? minutes: -1;
        
    }
};


```