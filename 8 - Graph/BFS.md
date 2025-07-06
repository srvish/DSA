# Breadth-First Search (BFS) Implementation in C#

## Algorithm Steps

- Represent the graph using either an adjacency list or an adjacency matrix.
- Use a queue to keep track of nodes to visit.
- Maintain a boolean array or set to mark visited nodes.
- **BFS Traversal:**
  - Enqueue the starting node and mark it as visited.
  - While the queue is not empty:
    - Dequeue a node from the queue.
    - Process the node (e.g., print or store it).
    - For each unvisited neighbor of the node:
      - Mark neighbor as visited and enqueue it.

---

## C# Code Example (Adjacency List)

```csharp
using System;
using System.Collections.Generic;

// BFS using adjacency list
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

    public void BFS(int start)
    {
        bool[] visited = new bool[vertices];
        Queue<int> queue = new Queue<int>();

        visited[start] = true;
        queue.Enqueue(start);

        while (queue.Count > 0)
        {
            int node = queue.Dequeue();
            Console.Write(node + " ");

            foreach (int neighbor in adjList[node])
            {
                if (!visited[neighbor])
                {
                    visited[neighbor] = true;
                    queue.Enqueue(neighbor);
                }
            }
        }
    }
}
```

---

## C# Code Example (Adjacency Matrix)

```csharp
using System;
using System.Collections.Generic;

// BFS using adjacency matrix
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

    public void BFS(int start)
    {
        bool[] visited = new bool[vertices];
        Queue<int> queue = new Queue<int>();

        visited[start] = true;
        queue.Enqueue(start);

        while (queue.Count > 0)
        {
            int node = queue.Dequeue();
            Console.Write(node + " ");

            for (int neighbor = 0; neighbor < vertices; neighbor++)
            {
                if (adjMatrix[node, neighbor] == 1 && !visited[neighbor])
                {
                    visited[neighbor] = true;
                    queue.Enqueue(neighbor);
                }
            }
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
