# Bellman-Ford Algorithm (Single Source Shortest Path) Implementation in C#

## Algorithm Steps

- Represent the graph as a list of edges (each edge has a source, destination, and weight).
- Initialize the distance to all vertices as infinity, except the source vertex (set to 0).
- For each vertex (V - 1) times:
  - For each edge (u, v, w):
    - If the distance to u is not infinity and distance to u + w < distance to v, update distance to v.
- Check for negative-weight cycles by iterating through all edges one more time:
  - If a shorter path is found, report that a negative-weight cycle exists.

---

## C# Code Example (Edge List)

```csharp
using System;
using System.Collections.Generic;

public class BellmanFord
{
    public class Edge
    {
        public int Src, Dest, Weight;
    }

    private int vertices;
    private List<Edge> edges = new List<Edge>();

    public BellmanFord(int v)
    {
        vertices = v;
    }

    public void AddEdge(int src, int dest, int weight)
    {
        edges.Add(new Edge { Src = src, Dest = dest, Weight = weight });
    }

    public void BellmanFordAlgo(int src)
    {
        int[] dist = new int[vertices];
        for (int i = 0; i < vertices; i++)
            dist[i] = int.MaxValue;
        dist[src] = 0;

        // Relax all edges |V| - 1 times
        for (int i = 1; i < vertices; i++)
        {
            foreach (var edge in edges)
            {
                if (dist[edge.Src] != int.MaxValue && dist[edge.Src] + edge.Weight < dist[edge.Dest])
                {
                    dist[edge.Dest] = dist[edge.Src] + edge.Weight;
                }
            }
        }

        // Check for negative-weight cycles
        foreach (var edge in edges)
        {
            if (dist[edge.Src] != int.MaxValue && dist[edge.Src] + edge.Weight < dist[edge.Dest])
            {
                Console.WriteLine("Graph contains negative weight cycle");
                return;
            }
        }

        PrintSolution(dist, src);
    }

    private void PrintSolution(int[] dist, int src)
    {
        Console.WriteLine("Vertex \tDistance from Source " + src);
        for (int i = 0; i < vertices; i++)
            Console.WriteLine($"{i}\t{(dist[i] == int.MaxValue ? "INF" : dist[i].ToString())}");
    }
}
```

---

## Time and Space Complexity

**Time Complexity**

- O(V \* E), where V is the number of vertices and E is the number of edges.

**Space Complexity**

- O(V), for the distance array.

## Uses

Bellman-Ford’s algorithm is used for:

- **Finding shortest paths** in graphs with negative edge weights.
- **Detecting negative-weight cycles** in a graph.
- **Network routing protocols** (e.g., RIP).
- **Currency arbitrage detection** in financial applications.
