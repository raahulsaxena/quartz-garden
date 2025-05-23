---
title: Graph Theory 
tags:
  - graph-theory
  - cycle-detection
  - topological-sort
  - shortest-path
description: Complete graph theory needed for coding interviews.
---


Author: Rahul Saxena
Last Updated: March 22, 2025

## Main topics to cover

1. **Graph Representation**
    - Adjacency Matrix
    - Adjacency List
2. **Graph Traversal**
    - BFS
    - DFS
3. **Topological Sort**
    - Using DFS
    - Kahn's Algorithm
4. **Cycle Detection**
    - Undirected Graph
    - Directed Graph
5. Bipartite Graph
6. **Shortest Path Algorithms**
    - Dijkstra's Algorithm
    - Bellman-Ford
    - Floyd-Warshall
7. **Union-Find / Disjoint Set**
8. **Minimum Spanning Tree**
    - Prim's Algorithm
    - Kruskal's Algorithm


![Graph Representation](Assets/adj_list.svg)
## <span style="color:red">Graph Representation</span>

### **1.  Adjacency Matrix**

Graph can be represented as a matrix where ```matrix[i][j]``` will have a value of 1 if there exists a edge between i and j and 0 otherwise.

### **2. Adjacency List**

Graph can also be represented as an adjacency list `adj` where `adj[i]` will store a list of neighbors of node `i`. (The list of nodes which share an edge with node `i`)

**C++ Code for both representations:**

```cpp

#include <iostream>
#include <vector>
using namespace std;


void adjacencyMatrix(int n, vector<vector<int>>& edges) {
    vector<vector<int>> adjMatrix(n, vector<int>(n, 0));
    for (auto& edge : edges) {
        int u = edge[0];
        int v = edge[1];
        adjMatrix[u][v] = 1;
        adjMatrix[v][u] = 1; 
    }

    for (auto row : adjMatrix) {
        for (auto val : row) cout << val << " ";
        cout << endl;
    }
}


void adjacencyList(int n, vector<vector<int>>& edges) {
    vector<vector<int>> adjList(n);
    for (auto& edge : edges) {
        int u = edge[0];
        int v = edge[1];
        adjList[u].push_back(v);
        adjList[v].push_back(u); 
    }

    for (int i = 0; i < n; i++) {
        cout << i << ": ";
        for (int v : adjList[i]) cout << v << " ";
        cout << endl;
    }
}

```

**Practice Problems:**

1. [LeetCode 133: Clone Graph](https://leetcode.com/problems/clone-graph/)
2. [LeetCode 797: All Paths From Source to Target](https://leetcode.com/problems/all-paths-from-source-to-target/)
3. [LeetCode 207: Course Schedule](https://leetcode.com/problems/course-schedule/)
4. [LeetCode 1557: Minimum Number of Vertices to Reach All Nodes](https://leetcode.com/problems/minimum-number-of-vertices-to-reach-all-nodes/)
5. [LeetCode 1466: Reorder Routes to Make All Paths Lead to the City Zero](https://leetcode.com/problems/reorder-routes-to-make-all-paths-lead-to-the-city-zero/)


---

![BFS DFS](Assets/bfs-dfs.png)
## Graph Traversals (BFS and DFS)

Graph traversal refers to the process of visiting all the nodes (vertices) in a graph systematically.

### **1. Breadth-First Search (BFS)**

**Breadth-First Search** is an algorithm that explores all the neighbors of a node before moving on to their children. It starts at a given node and explores all its neighbors first, before moving on to their neighbors, and so on.  

**Key Features:**
• **Level-order traversal**: BFS visits nodes level by level.
• **Queue-based**: It uses a queue to manage the nodes being explored, ensuring that nodes are explored in the correct order.
• **Shortest Path**: BFS is often used to find the shortest path in an unweighted graph because it explores all nodes at the present depth level before moving to nodes at the next depth level.

**Time and Space Complexity:**

• **Time Complexity**: **O(V + E)**:  where **V** is the number of vertices (nodes) and **E** is the number of edges. In BFS, each vertex and edge is processed exactly once.

• **Space Complexity**: **O(V)**:  BFS uses a queue to store nodes at each level, so the space required is proportional to the number of vertices in the graph.

### **2. Depth-First Search (DFS)**

**Depth-First Search** explores as far as possible along each branch before backtracking. DFS dives deep into the graph, visiting a node and then its neighbor, continuing until it can’t go any further, and then it backtracks to explore other paths.

**Key Features:**

• **Recursive or Stack-based**: DFS can be implemented using recursion or an explicit stack data structure.
• **Pathfinding**: Unlike BFS, DFS doesn’t necessarily find the shortest path but can be useful in problems requiring a full exploration of all paths.
• **Tree Structure**: DFS works well in tree structures, where we traverse down to the deepest node before visiting siblings.

**Time and Space Complexity:**

• **Time Complexity**: **O(V + E)**:  Like BFS, DFS also processes every vertex and edge exactly once, leading to a time complexity of **O(V + E)**.

• **Space Complexity**: **O(V)**:  In the worst case, DFS needs to store all the vertices in the recursion stack (or stack used in the iterative implementation), leading to a space complexity of **O(V)**. The depth of recursion could go up to **V** in case of deep graphs.

### **C++ Code:**

```cpp
#include <iostream>
#include <vector>
#include <queue>
using namespace std;

// BFS
void bfs(int start, vector<vector<int>>& adjList, int n) {
    vector<bool> visited(n, false);
    queue<int> q;
    q.push(start);
    visited[start] = true;

    while (!q.empty()) {
        int node = q.front();
        q.pop();
        cout << node << " ";

        for (int neighbor : adjList[node]) {
            if (!visited[neighbor]) {
                q.push(neighbor);
                visited[neighbor] = true;
            }
        }
    }
}

// DFS
void dfs(int node, vector<vector<int>>& adjList, vector<bool>& visited) {
    visited[node] = true;
    cout << node << " ";

    for (int neighbor : adjList[node]) {
        if (!visited[neighbor]) {
            dfs(neighbor, adjList, visited);
        }
    }
}

```

**Practice Problems:**

1. [LeetCode 200: Number of Islands](https://leetcode.com/problems/number-of-islands/)
2. [LeetCode 994: Rotting Oranges](https://leetcode.com/problems/rotting-oranges/)
3. [LeetCode 103: Binary Tree Zigzag Level Order Traversal](https://leetcode.com/problems/binary-tree-zigzag-level-order-traversal/)
4. [LeetCode 130: Surrounded Regions](https://leetcode.com/problems/surrounded-regions/)
5. [LeetCode 1306: Jump Game III](https://leetcode.com/problems/jump-game-iii/)

---

![Topo Sort](Assets/topo-sort.png)
## **Topological Sort**

Topological Sorting is a **linear ordering of vertices** in a **Directed Acyclic Graph (DAG)** such that for every directed edge `u` to `v`, vertex `u` comes **before** vertex `v` in the ordering. 

Properties:
- It only exists in a directed acyclic graph.
- A graph can have multiple valid topological sort orders.
- This is commonly used in task scheduling, dependency resolution.

### **1. Using DFS**

The idea behind topological sorting using DFS is based on the fact that in a DAG, when you perform a DFS traversal, you explore a node’s neighbors first, marking each node as visited, and after exploring all its neighbors, you push it onto a stack (or a result list). Once all the nodes are explored, the stack will contain the nodes in the reverse order of their finishing times, which gives us a **valid topological order**.

### **2. Kahn's Algorithm**

Kahn's Algorithm is an approach similar to BFS to return the topological sort of the graph. It uses the concept of indegrees and outdegrees to provide the ordering.

**C++ Code:**

```cpp
#include <iostream>#include <vector>#include <stack>#include <queue>using namespace std;

// Topological Sort using DFS
void topoSortDFS(int node, vector<vector<int>>& adjList, vector<bool>& visited, stack<int>& st) {
    visited[node] = true;

    for (int neighbor : adjList[node]) {
        if (!visited[neighbor]) {
            topoSortDFS(neighbor, adjList, visited, st);
        }
    }
    st.push(node);
}

vector<int> topologicalSortDFS(int n, vector<vector<int>>& adjList) {
    vector<bool> visited(n, false);
    stack<int> st;
    for (int i = 0; i < n; i++) {
        if (!visited[i]) {
            topoSortDFS(i, adjList, visited, st);
        }
    }

    vector<int> topoOrder;
    while (!st.empty()) {
        topoOrder.push_back(st.top());
        st.pop();
    }
    return topoOrder;
}

// Topological Sort using Kahn's Algorithm (BFS)
vector<int> topologicalSortKahn(int n, vector<vector<int>>& adjList) {
    vector<int> inDegree(n, 0);
    for (int i = 0; i < n; i++) {
        for (int neighbor : adjList[i]) {
            inDegree[neighbor]++;
        }
    }

    queue<int> q;
    for (int i = 0; i < n; i++) {
        if (inDegree[i] == 0) q.push(i);
    }

    vector<int> topoOrder;
    while (!q.empty()) {
        int node = q.front();
        q.pop();
        topoOrder.push_back(node);

        for (int neighbor : adjList[node]) {
            inDegree[neighbor]--;
            if (inDegree[neighbor] == 0) q.push(neighbor);
        }
    }
    return topoOrder;
}

```

**Practice Problems:**

1. [LeetCode 210: Course Schedule II](https://leetcode.com/problems/course-schedule-ii/)
2. [LeetCode 802: Find Eventual Safe States](https://leetcode.com/problems/find-eventual-safe-states/)
3. [LeetCode 329: Longest Increasing Path in a Matrix](https://leetcode.com/problems/longest-increasing-path-in-a-matrix/)
4. [LeetCode 1136: Parallel Courses](https://leetcode.com/problems/parallel-courses/)
5. [LeetCode 1203: Sort Items by Groups Respecting Dependencies](https://leetcode.com/problems/sort-items-by-groups-respecting-dependencies/)


---

![Cycle Detection](Assets/cycle-detection-graph.png)
## **Cycle Detection**

Cycle detection is a fundamental problem in graph theory, aiming to determine whether a given graph contains any cycles. A **cycle** in a graph is a path that starts and ends at the same vertex, with all edges being distinct.

### **1. Undirected Graph**

In undirected graphs, detecting a cycle is slightly more straightforward. Since the edges have no direction, we can simply check for back edges (edges that point back to an ancestor node) during a Depth-First Search (DFS).

**Steps (DFS-based):**

1. Perform a DFS traversal of the graph, keeping track of visited vertices.
2. For each vertex, check all its adjacent vertices.
3. If an adjacent vertex has been visited and is not the parent of the current vertex, a cycle is detected.
4. Repeat this process for all vertices to ensure the entire graph is checked.

  

**Time Complexity:**

• The time complexity is **O(V + E)**, where **V** is the number of vertices and **E** is the number of edges.

### **2. Directed Graph**

In directed graphs, cycle detection is more complex due to the directed nature of the edges. A cycle occurs if there’s a path from a node back to itself, following the direction of edges. We can detect cycles in directed graphs using DFS, but with additional tracking of the recursion stack to identify back edges (edges that point back to a node in the current DFS path).


**Steps (DFS-based):**
1. Perform a DFS traversal of the graph.
2. Maintain two auxiliary arrays:
	• **Visited:** Tracks whether a node has been visited.
	• **Recursion Stack:** Tracks the nodes currently in the recursion stack (i.e., the path being explored).
3. For each node, mark it as visited and add it to the recursion stack.
4. For each adjacent vertex, if it has been visited and is currently in the recursion stack, a cycle is detected.
5. On backtracking, remove the node from the recursion stack.
6. Repeat this process for all vertices to ensure the entire graph is checked.

  

**Time Complexity:**

• The time complexity is **O(V + E)**, where **V** is the number of vertices and **E** is the number of edges.

**C++ Code:**

```cpp
#include <iostream>#include <vector>using namespace std;

// Cycle Detection in Undirected Graph using DFS
bool isCyclicDFS(int node, int parent, vector<vector<int>>& adjList, vector<bool>& visited) {
    visited[node] = true;

    for (int neighbor : adjList[node]) {
        if (!visited[neighbor]) {
            if (isCyclicDFS(neighbor, node, adjList, visited)) {
                return true;
            }
        } else if (neighbor != parent) {
            return true;
        }
    }
    return false;
}

bool hasCycleUndirected(int n, vector<vector<int>>& adjList) {
    vector<bool> visited(n, false);

    for (int i = 0; i < n; i++) {
        if (!visited[i]) {
            if (isCyclicDFS(i, -1, adjList, visited)) {
                return true;
            }
        }
    }
    return false;
}

// Cycle Detection in Directed Graph using DFS
bool isCyclicDFSDirected(int node, vector<vector<int>>& adjList, vector<bool>& visited, vector<bool>& recStack) {
    visited[node] = true;
    recStack[node] = true;

    for (int neighbor : adjList[node]) {
        if (!visited[neighbor] && isCyclicDFSDirected(neighbor, adjList, visited, recStack)) {
            return true;
        } else if (recStack[neighbor]) {
            return true;
        }
    }
    recStack[node] = false;
    return false;
}

bool hasCycleDirected(int n, vector<vector<int>>& adjList) {
    vector<bool> visited(n, false);
    vector<bool> recStack(n, false);

    for (int i = 0; i < n; i++) {
        if (!visited[i]) {
            if (isCyclicDFSDirected(i, adjList, visited, recStack)) {
                return true;
            }
        }
    }
    return false;
}

```

**Practice Problems:**

1. [LeetCode 785: Is Graph Bipartite?](https://leetcode.com/problems/is-graph-bipartite/)
2. [LeetCode 207: Course Schedule](https://leetcode.com/problems/course-schedule/) _(Directed Graph Cycle Detection)_
3. [LeetCode 261: Graph Valid Tree](https://leetcode.com/problems/graph-valid-tree/)
4. [LeetCode 802: Find Eventual Safe States](https://leetcode.com/problems/find-eventual-safe-states/) _(Directed Graph Cycle Detection)_
5. [LeetCode 1462: Course Schedule IV](https://leetcode.com/problems/course-schedule-iv/) _(Cycle detection in multiple queries)_

---

![Bipartite](Assets/bipartite.png)
## **Bipartite Graph**

A graph is bipartite if it can be **2-colored**, meaning that it is possible to assign one color to one set of vertices and a different color to the other set. If during a DFS or BFS traversal, we can color the graph in two colors without conflicts, the graph is bipartite. If we find that a vertex must be the same color as one of its neighbors, then the graph contains an odd-length cycle, and thus it is not bipartite.

**Algorithm for Checking Bipartiteness:**

1. **BFS-based Approach:**

	• Start by coloring any vertex with one color (say, color 1).
	• Use BFS to visit all vertices.
	• For each vertex, color its unvisited neighbors with the opposite color (color 2).
	• If you encounter a vertex that is already colored the same as the current vertex, the graph is **not bipartite** (contains an odd-length cycle).

2. **DFS-based Approach:**

	• Start from any unvisited vertex and assign a color to it.
	• Recursively color all its neighbors with the opposite color.
	• If any vertex is found to be colored the same as one of its neighbors, the graph is **not bipartite**.


**Time Complexity:**

• Both the BFS and DFS approaches run in **O(V + E)** time, where **V** is the number of vertices and **E** is the number of edges. This is because each vertex and edge is processed once during the traversal.


**C++ Code:**

```cpp
#include <iostream>
#include <vector>
#include <queue>
using namespace std;

// Check if Graph is Bipartite using BFS
bool isBipartite(int n, vector<vector<int>>& adjList) {
    vector<int> color(n, -1);

    for (int i = 0; i < n; i++) {
        if (color[i] == -1) {
            queue<int> q;
            q.push(i);
            color[i] = 0;

            while (!q.empty()) {
                int node = q.front();
                q.pop();

                for (int neighbor : adjList[node]) {
                    if

 (color[neighbor] == -1) {
                        color[neighbor] = 1 - color[node];
                        q.push(neighbor);
                    } else if (color[neighbor] == color[node]) {
                        return false;
                    }
                }
            }
        }
    }
    return true;
}

```

**Practice Problems:**

1. [LeetCode 785: Is Graph Bipartite?](https://leetcode.com/problems/is-graph-bipartite/)
2. [LeetCode 886: Possible Bipartition](https://leetcode.com/problems/possible-bipartition/)
3. [LeetCode 1034: Coloring A Border](https://leetcode.com/problems/coloring-a-border/)
4. [LeetCode 994: Rotting Oranges](https://leetcode.com/problems/rotting-oranges/) _(BFS based problem)_
5. [LeetCode 1091: Shortest Path in Binary Matrix](https://leetcode.com/problems/shortest-path-in-binary-matrix/)


---

![Shortest Path](Assets/djikstra.png)

## **Shortest Path Algorithms**

The **Shortest Path Problem** involves finding the path between two vertices in a graph such that the total edge weight is minimized. There are several algorithms designed to solve this problem, each suitable for different types of graphs. The three most commonly used shortest path algorithms are **Dijkstra’s Algorithm**, **Bellman-Ford Algorithm**, and **Floyd-Warshall Algorithm**.

### **1. Dijkstra's Algorithm**

**Dijkstra’s Algorithm** is a greedy algorithm that solves the single-source shortest path problem for a graph with non-negative edge weights. It finds the shortest path from a source vertex to all other vertices in the graph.

**Steps:**

1. Initialize the distance to the source vertex as 0 and all other vertices as infinity.
2. Use a priority queue (min-heap) to repeatedly select the vertex with the smallest tentative distance.
3. For the selected vertex, update the tentative distances of its neighbors.
4. Repeat the process until all vertices have been visited.

**Limitations:**

• Dijkstra’s algorithm only works with non-negative edge weights. It doesn’t handle graphs with negative weights.


**Time Complexity:**

• Using a simple array: **O(V^2)**.
• Using a priority queue (min-heap) and adjacency list: **O((V + E) log V)**, where **V** is the number of vertices and **E** is the number of edges.

### **2. Bellman-Ford**

**Bellman-Ford Algorithm** is an algorithm that computes the shortest paths from a single source vertex to all other vertices, and it can handle graphs with negative edge weights. It also detects negative weight cycles in the graph. It is slower than Djikstra's algorithm for a graph without negative weights.

**Steps:**

1. Initialize the distance to the source vertex as 0 and all other vertices as infinity.
2. Relax all edges **V-1** times, where **V** is the number of vertices. Relaxing an edge means updating the distance to the destination vertex if a shorter path is found.
3. Check for negative weight cycles. If any edge can still be relaxed after **V-1** iterations, a negative weight cycle exists.

**Time Complexity:**

• **O(V * E)**, where **V** is the number of vertices and **E** is the number of edges.

### **3. Floyd-Warshall**

**Floyd-Warshall Algorithm** is a dynamic programming algorithm used to find the shortest paths between all pairs of vertices in a graph. It works for both directed and undirected graphs and can handle graphs with negative edge weights as long as there are no negative weight cycles. It can be ideal when you want to compute all-pairs shortest path.

**Steps:**

1. Create a distance matrix where each entry `dist[i][j]` holds the shortest distance between vertex `i` and vertex `j`.
2. Initialize the distance matrix with the edge weights for direct connections, and set all other distances to infinity.
3. For each vertex **k**, update the matrix to check if a path through **k** provides a shorter path between vertices `i` and  `j`.
4. Repeat this process for every vertex as an intermediate vertex.

**Time Complexity:**

• **O(V^3)**, where **V** is the number of vertices.

**C++ Code:**

```cpp
#include <iostream>#include <vector>#include <queue>#include <climits>using namespace std;

// Dijkstra's Algorithm
vector<int> dijkstra(int n, vector<vector<pair<int, int>>>& adjList, int start) {
    vector<int> dist(n, INT_MAX);
    priority_queue<pair<int, int>, vector<pair<int, int>>, greater<pair<int, int>>> pq;
    dist[start] = 0;
    pq.push({0, start});

    while (!pq.empty()) {
        int u = pq.top().second;
        pq.pop();

        for (auto& neighbor : adjList[u]) {
            int v = neighbor.first;
            int weight = neighbor.second;

            if (dist[u] + weight < dist[v]) {
                dist[v] = dist[u] + weight;
                pq.push({dist[v], v});
            }
        }
    }
    return dist;
}

// Bellman-Ford Algorithm
vector<int> bellmanFord(int n, vector<vector<int>>& edges, int start) {
    vector<int> dist(n, INT_MAX);
    dist[start] = 0;

    for (int i = 1; i <= n - 1; i++) {
        for (auto& edge : edges) {
            int u = edge[0];
            int v = edge[1];
            int weight = edge[2];

            if (dist[u] != INT_MAX && dist[u] + weight < dist[v]) {
                dist[v] =

 dist[u] + weight;
            }
        }
    }
    return dist;
}

// Floyd-Warshall Algorithm
vector<vector<int>> floydWarshall(int n, vector<vector<int>>& graph) {
    vector<vector<int>> dist = graph;

    for (int k = 0; k < n; k++) {
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++) {
                if (dist[i][k] != INT_MAX && dist[k][j] != INT_MAX && dist[i][k] + dist[k][j] < dist[i][j]) {
                    dist[i][j] = dist[i][k] + dist[k][j];
                }
            }
        }
    }
    return dist;
}

```

**Practice Problems:**

1. [LeetCode 743: Network Delay Time](https://leetcode.com/problems/network-delay-time/)
2. [LeetCode 787: Cheapest Flights Within K Stops](https://leetcode.com/problems/cheapest-flights-within-k-stops/)
3. [LeetCode 1631: Path With Minimum Effort](https://leetcode.com/problems/path-with-minimum-effort/)
4. [LeetCode 1514: Path with Maximum Probability](https://leetcode.com/problems/path-with-maximum-probability/)
5. [LeetCode 1129: Shortest Path with Alternating Colors](https://leetcode.com/problems/shortest-path-with-alternating-colors/)

---

![Union-Find](Assets/union-find.png)
## **Union-Find / Disjoint Set**

Union Find, also known as **Disjoint Set Union (DSU)**, is a data structure used to efficiently manage and merge disjoint sets, supporting two primary operations:

1. **Find:** Determines which set a particular element belongs to.
2. **Union:** Merges two sets into one, if they are not already connected.


It is commonly used in algorithms that deal with dynamic connectivity problems, such as detecting cycles in graphs, finding connected components, and Kruskal’s algorithm for finding the Minimum Spanning Tree (MST) of a graph.


**C++ Code:**

```cpp
#include <iostream>
#include <vector>
using namespace std;

class UnionFind {
private:
    vector<int> parent;
    vector<int> rank;

public:
    UnionFind(int n) {
        parent.resize(n);
        rank.resize(n, 0);
        for (int i = 0; i < n; i++) {
            parent[i] = i;
        }
    }

    int find(int x) {
        if (parent[x] != x) {
            parent[x] = find(parent[x]); // Path compression
        }
        return parent[x];
    }

    void unionSets(int x, int y) {
        int rootX = find(x);
        int rootY = find(y);

        if (rootX != rootY) {
            if (rank[rootX] > rank[rootY]) {
                parent[rootY] = rootX;
            } else if (rank[rootX] < rank[rootY]) {
                parent[rootX] = rootY;
            } else {
                parent[rootY] = rootX;
                rank[rootX]++;
            }
        }
    }
};

```

**Practice Problems:**

1. [LeetCode 684: Redundant Connection](https://leetcode.com/problems/redundant-connection/)
2. [LeetCode 990: Satisfiability of Equality Equations](https://leetcode.com/problems/satisfiability-of-equality-equations/)
3. [LeetCode 721: Accounts Merge](https://leetcode.com/problems/accounts-merge/)
4. [LeetCode 1319: Number of Operations to Make Network Connected](https://leetcode.com/problems/number-of-operations-to-make-network-connected/)
5. [LeetCode 128: Longest Consecutive Sequence](https://leetcode.com/problems/longest-consecutive-sequence/)

---


![MST](Assets/mst.jpg)
## **Minimum Spanning Tree**


A **Minimum Spanning Tree (MST)** of a weighted, connected graph is a subset of edges that connects all the vertices together without any cycles and with the minimum possible total edge weight. The MST is essential in various real-world applications such as network design, clustering, and circuit design.

### **1. Prim's Algorithm**

Prim’s Algorithm is a **greedy** algorithm that grows the MST incrementally. Starting from an arbitrary node, it repeatedly adds the smallest edge that connects a vertex in the tree to a vertex outside the tree, ensuring no cycles are formed.


**Steps:**
1. Start with an arbitrary vertex and add it to the MST.
2. Choose the edge with the minimum weight that connects a vertex in the MST to a vertex outside it.
3. Add the chosen edge and vertex to the MST.
4. Repeat steps 2-3 until all vertices are included in the MST.

**Time Complexity:**

• Using an adjacency matrix, the time complexity is `O(V^2)`.
• Using a priority queue (min-heap) and adjacency list, the time complexity is `O(E log V)`, where **V** is the number of vertices and **E** is the number of edges.

### **2. Kruskal's Algorithm**

Kruskal’s Algorithm is another **greedy** algorithm that builds the MST by considering edges in increasing order of weight. It processes all the edges first, adding them one by one to the MST if they don’t form a cycle, typically using a **Union-Find** data structure to detect cycles.

**Steps:**
1. Sort all edges in non-decreasing order of their weights.
2. Initialize an empty set for the MST.
3. Pick the smallest edge from the sorted edge list. If adding it to the MST doesn’t form a cycle, include it.
4. Repeat until the MST contains **V-1** edges (for a graph with **V** vertices).

  

**Time Complexity:**
• Sorting the edges takes **O(E log E)** time.
• Union-Find operations (with path compression and union by rank) take **O(E log V)** time.
• Overall, the time complexity is **O(E log E)** or **O(E log V)**, where **V** is the number of vertices and **E** is the number of edges.


**C++ Code:**

```cpp

#include <iostream>
#include <vector>
#include <queue>
#include <algorithm>
using namespace std;

// Prim's Algorithm
int primMST(int n, vector<vector<pair<int, int>>>& adjList) {
    vector<bool> inMST(n, false);
    priority_queue<pair<int, int>, vector<pair<int, int>>, greater<pair<int, int>>> pq;
    int mstCost = 0;

    pq.push({0, 0}); // (cost, node)

    while (!pq.empty()) {
        int u = pq.top().second;
        int cost = pq.top().first;
        pq.pop();

        if (inMST[u]) continue;

        mstCost += cost;
        inMST[u] = true;

        for (auto& neighbor : adjList[u]) {
            int v = neighbor.first;
            int weight = neighbor.second;

            if (!inMST[v]) {
                pq.push({weight, v});
            }
        }
    }
    return mstCost;
}

// Kruskal's Algorithm
class Edge {
public:
    int u, v, weight;
    Edge(int _u, int _v, int _weight) : u(_u), v(_v), weight(_weight) {}
};

bool compare(Edge e1, Edge e2) {
    return e1.weight < e2.weight;
}

int kruskalMST(int n, vector<Edge>& edges) {
    sort(edges.begin(), edges.end(), compare);
    UnionFind uf(n);
    int mstCost = 0;

    for (auto& edge : edges) {
        if (uf.find(edge.u) != uf.find(edge.v)) {
            mstCost += edge.weight;
            uf.unionSets(edge.u, edge.v);
        }
    }
    return mstCost;
}

```

**Practice Problems:**

1. [LeetCode 1584: Min Cost to Connect All Points](https://leetcode.com/problems/min-cost-to-connect-all-points/)
2. [LeetCode 1135: Connecting Cities With Minimum Cost](https://leetcode.com/problems/connecting-cities-with-minimum-cost/)
3. [LeetCode 1631: Path With Minimum Effort](https://leetcode.com/problems/path-with-minimum-effort/) _(Can be solved with MST)_
4. [LeetCode 1101: The Earliest Moment When Everyone Become Friends](https://leetcode.com/problems/the-earliest-moment-when-everyone-become-friends/)
5. [LeetCode 1579: Remove Max Number of Edges to Keep Graph Fully Traversable](https://leetcode.com/problems/remove-max-number-of-edges-to-keep-graph-fully-traversable/)
