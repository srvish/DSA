# Depth-First Search (DFS) Implementation in C#

## Algorithm Steps

- Represent the graph using either an adjacency list or an adjacency matrix.
- Use a stack (explicit or via recursion) to keep track of nodes to visit.
- Maintain a boolean array or set to mark visited nodes.
- **DFS Traversal:**
  - Start from the given node, mark it as visited, and process it.
  - For each unvisited neighbor of the node:
    - Recursively (or using a stack) visit the neighbor.

---

## C# Code Example (Adjacency List)

```csharp
using System;
using System.Collections.Generic;

// DFS using adjacency list (recursive)
public class GraphList
{
    private int vertices;
    private List<int>[] adjList;

    public GraphList(int v)
    {
        vertices = v;
        adjList = new List<int>[v];
        for (int i = 0; i < v; i++)
            adjList[i] = new List<int>();
    }

    public void AddEdge(int u, int v)
    {
        adjList[u].Add(v);
        adjList[v].Add(u); // For undirected graph
    }

    public void DFS(int start)
    {
        bool[] visited = new bool[vertices];
        DFSUtil(start, visited);
    }

    private void DFSUtil(int node, bool[] visited)
    {
        visited[node] = true;
        Console.Write(node + " ");

        foreach (int neighbor in adjList[node])
        {
            if (!visited[neighbor])
                DFSUtil(neighbor, visited);
        }
    }
}
```

---

## C# Code Example (Adjacency Matrix)

```csharp
using System;
using System.Collections.Generic;

// DFS using adjacency matrix (recursive)
public class GraphMatrix
{
    private int vertices;
    private int[,] adjMatrix;

    public GraphMatrix(int v)
    {
        vertices = v;
        adjMatrix = new int[v, v];
    }

    public void AddEdge(int u, int v)
    {
        adjMatrix[u, v] = 1;
        adjMatrix[v, u] = 1; // For undirected graph
    }

    public void DFS(int start)
    {
        bool[] visited = new bool[vertices];
        DFSUtil(start, visited);
    }

    private void DFSUtil(int node, bool[] visited)
    {
        visited[node] = true;
        Console.Write(node + " ");

        for (int neighbor = 0; neighbor < vertices; neighbor++)
        {
            if (adjMatrix[node, neighbor] == 1 && !visited[neighbor])
                DFSUtil(neighbor, visited);
        }
    }
}
```

---

## Time and Space Complexity

**Time Complexity**

- **Adjacency List:** O(V + E), where V is the number of vertices and E is the number of edges.
- **Adjacency Matrix:** O(V²), since each vertex checks all possible neighbors.

**Space Complexity**

- **Adjacency List:** O(V + E)
