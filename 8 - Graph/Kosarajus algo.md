# Kosaraju’s Algorithm (Strongly Connected Components) Implementation in C#

## Algorithm Steps

- Represent the graph using an adjacency list.
- **First DFS Pass:**
  - Perform DFS traversal of the original graph, pushing each finished vertex onto a stack.
- **Transpose the Graph:**
  - Reverse the direction of all edges to get the transpose graph.
- **Second DFS Pass:**
  - Pop vertices one by one from the stack and perform DFS on the transposed graph.
  - Each DFS traversal in this step gives one strongly connected component (SCC).

---

## C# Code Example (Adjacency List)

```csharp
using System;
using System.Collections.Generic;

public class KosarajuSCC
{
    private int vertices;
    private List<int>[] adjList;

    public KosarajuSCC(int v)
    {
        vertices = v;
        adjList = new List<int>[v];
        for (int i = 0; i < v; i++)
            adjList[i] = new List<int>();
    }

    public void AddEdge(int u, int v)
    {
        adjList[u].Add(v);
    }

    // First DFS pass to fill stack by finish time
    private void FillOrder(int v, bool[] visited, Stack<int> stack)
    {
        visited[v] = true;
        foreach (int neighbor in adjList[v])
            if (!visited[neighbor])
                FillOrder(neighbor, visited, stack);
        stack.Push(v);
    }

    // Transpose the graph
    private KosarajuSCC GetTranspose()
    {
        KosarajuSCC gT = new KosarajuSCC(vertices);
        for (int v = 0; v < vertices; v++)
            foreach (int neighbor in adjList[v])
                gT.adjList[neighbor].Add(v);
        return gT;
    }

    // DFS for the transposed graph
    private void DFSUtil(int v, bool[] visited)
    {
        visited[v] = true;
        Console.Write(v + " ");
        foreach (int neighbor in adjList[v])
            if (!visited[neighbor])
                DFSUtil(neighbor, visited);
    }

    public void PrintSCCs()
    {
        Stack<int> stack = new Stack<int>();
        bool[] visited = new bool[vertices];

        // Fill vertices in stack according to their finishing times
        for (int i = 0; i < vertices; i++)
            if (!visited[i])
                FillOrder(i, visited, stack);

        // Create a reversed graph
        KosarajuSCC gr = GetTranspose();

        // Mark all vertices as not visited for the second DFS
        for (int i = 0; i < vertices; i++)
            visited[i] = false;

        // Process all vertices in order defined by Stack
        while (stack.Count > 0)
        {
            int v = stack.Pop();
            if (!visited[v])
            {
                gr.DFSUtil(v, visited);
                Console.WriteLine();
            }
        }
    }
}
```

---

## Time and Space Complexity

**Time Complexity**

- O(V + E), where V is the number of vertices and E is the number of edges.

**Space Complexity**

- O(V + E), for storing the graph and its transpose.

## Uses

Kosaraju’s algorithm is used for:

- **Finding strongly connected components** in directed graphs.
- **Analyzing web pages** (finding clusters of mutually reachable pages).
- **Program analysis** (finding cycles in call graphs or dependency graphs).
- **Deadlock detection** in operating systems.