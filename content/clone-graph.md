---
title: Clone Graph (Leetcode 133)
tags:
  - graph
  - BFS
  - Leetcode
  - deep copy
  - problems
description: Given a node in a connected undirected graph, return a deep copy of the graph. Leetcode 133.
---

## Question
---

Given a node in a connected undirected graph, return a deep copy of the graph.

Each node in the graph contains an integer value and a list of its neighbors.

```java
class Node {
    public int val;
    public List<Node> neighbors;
}
```


The graph is shown in the test cases as an adjacency list. **An adjacency list** is a mapping of nodes to lists, used to represent a finite graph. Each list describes the set of neighbors of a node in the graph.

For simplicity, nodes values are numbered from 1 to `n`, where `n` is the total number of nodes in the graph. The index of each node within the adjacency list is the same as the node's value (1-indexed).

The input node will always be the first node in the graph and have `1` as the value.

**Example 1:**

![](https://imagedelivery.net/CLfkmk9Wzy8_9HRyug4EVA/ca68c09d-4d0e-4d80-9c20-078c666cf900/public)

```java
Input: adjList = [[2],[1,3],[2]]

Output: [[2],[1,3],[2]]
```

Copy

Explanation: There are 3 nodes in the graph.  
Node 1: val = 1 and neighbors = [2].  
Node 2: val = 2 and neighbors = [1, 3].  
Node 3: val = 3 and neighbors = [2].

**Example 2:**

![](https://imagedelivery.net/CLfkmk9Wzy8_9HRyug4EVA/96c7fb34-26e8-42e0-5f5d-61b8b8c96800/public)

```java
Input: adjList = [[]]

Output: [[]]
```

Copy

Explanation: The graph has one node with no neighbors.

**Example 3:**

```java
Input: adjList = []

Output: []
```

Copy

Explanation: The graph is empty.

**Constraints:**

- `0 <= The number of nodes in the graph <= 100`.
- `1 <= Node.val <= 100`
- There are no duplicate edges and no self-loops in the graph.

## Solution:
---

### Algorithms/Patterns
- [[BFS on graph]]

### Common Mistakes
- Not using a map to avoid copying a node twice. Graph can contain cycles.

### Code:
```python

"""
# Definition for a Node.
class Node:
    def __init__(self, val = 0, neighbors = None):
        self.val = val
        self.neighbors = neighbors if neighbors is not None else []
"""

class Solution:
    def cloneGraph(self, node: Optional['Node']) -> Optional['Node']:

        if not node:
            return None

        visited = {}

        visited[node] = Node(node.val)

        q = deque([node])

        while q:

            curr = q.popleft()

            for neighbor in curr.neighbors:
                
                if neighbor not in visited:
                    q.append(neighbor)
                    visited[neighbor] = Node(neighbor.val)
                
                visited[curr].neighbors.append(visited[neighbor])

        return visited[node]
```