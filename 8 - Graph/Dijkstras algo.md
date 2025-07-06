# Dijkstra’s Algorithm (Shortest Path) Implementation in C#

## Algorithm Steps

- Represent the graph using an adjacency matrix or adjacency list.
- Create an array `dist[]` to store the shortest distance from the source to each vertex, initialized to infinity except for the source (set to 0).
- Create a boolean array `sptSet[]` to track vertices included in the shortest path tree.
- For all vertices:
  - Pick the vertex `u` not yet included in `sptSet` with the minimum distance value.
  - Mark `u` as included in `sptSet`.
  - Update the distance value of all adjacent vertices of `u` if a shorter path is found through `u`.

---

## C# Code Example (Adjacency Matrix)

```csharp
using System;

public class Dijkstra
{
    private int vertices;

    public Dijkstra(int v)
    {
        vertices = v;
    }

    // Find the vertex with the minimum distance value not yet included in sptSet
    private int MinDistance(int[] dist, bool[] sptSet)
    {
        int min = int.MaxValue, minIndex = -1;
        for (int v = 0; v < vertices; v++)
        {
            if (!sptSet[v] && dist[v] <= min)
            {
                min = dist[v];
                minIndex = v;
            }
        }
        return minIndex;
    }

    // Print the constructed shortest distance array
    private void PrintSolution(int[] dist, int src)
    {
        Console.WriteLine("Vertex \tDistance from Source " + src);
        for (int i = 0; i < vertices; i++)
            Console.WriteLine($"{i}\t{dist[i]}");
    }

    public void DijkstraAlgo(int[,] graph, int src)
    {
        int[] dist = new int[vertices]; // The output array. dist[i] will hold the shortest distance from src to i
        bool[] sptSet = new bool[vertices]; // sptSet[i] will be true if vertex i is included in shortest path tree

        for (int i = 0; i < vertices; i++)
        {
            dist[i] = int.MaxValue;
            sptSet[i] = false;
        }

        dist[src] = 0;

        for (int count = 0; count < vertices - 1; count++)
        {
            int u = MinDistance(dist, sptSet);
            sptSet[u] = true;

            for (int v = 0; v < vertices; v++)
            {
                if (!sptSet[v] && graph[u, v] != 0 && dist[u] != int.MaxValue && dist[u] + graph[u, v] < dist[v])
                {
                    dist[v] = dist[u] + graph[u, v];
                }
            }
        }

        PrintSolution(dist, src);
    }
}
```

---

## Time and Space Complexity

**Time Complexity**

- O(V²), where V is the number of vertices (for adjacency matrix implementation).

**Space Complexity**

- O(V), for the distance and sptSet arrays.

## Uses

Dijkstra’s algorithm is used for:

- **Finding the shortest path** in weighted graphs (with non-negative weights).
- **Network routing protocols** (e.g., OSPF, IS-IS).
- **Map and GPS navigation systems**.
- **Resource optimization** in various applications.
