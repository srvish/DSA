# Floyd-Warshall Algorithm

## What is Floyd-Warshall?

The **Floyd-Warshall algorithm** is a dynamic programming algorithm used to find the shortest paths between all pairs of vertices in a weighted graph (can handle negative edge weights, but no negative cycles). It is especially useful for dense graphs and is simple to implement.

**Applications:**

- All-pairs shortest path in graphs
- Transitive closure of a directed graph
- Finding the minimum cost between every pair of cities/nodes

---

## Algorithm Steps

- Represent the graph using an adjacency matrix `dist`, where `dist[i][j]` is the weight of the edge from vertex `i` to vertex `j` (or infinity if no edge).
- For each vertex `k` (as an intermediate vertex):
  - For each pair of vertices `(i, j)`:
    - If `dist[i][k] + dist[k][j] < dist[i][j]`, update `dist[i][j] = dist[i][k] + dist[k][j]`.
- After all iterations, `dist[i][j]` contains the shortest distance from `i` to `j`.

---

## C# Code Example

```csharp
using System;

public class FloydWarshall
{
    public static void FloydWarshallAlgo(int[,] graph, int V)
    {
        int[,] dist = new int[V, V];

        // Initialize the solution matrix same as input graph matrix
        for (int i = 0; i < V; i++)
            for (int j = 0; j < V; j++)
                dist[i, j] = graph[i, j];

        // Add all vertices one by one to the set of intermediate vertices
        for (int k = 0; k < V; k++)
        {
            for (int i = 0; i < V; i++)
            {
                for (int j = 0; j < V; j++)
                {
                    if (dist[i, k] != int.MaxValue && dist[k, j] != int.MaxValue
                        && dist[i, k] + dist[k, j] < dist[i, j])
                    {
                        dist[i, j] = dist[i, k] + dist[k, j];
                    }
                }
            }
        }

        // Print the shortest distance matrix
        PrintSolution(dist, V);
    }

    private static void PrintSolution(int[,] dist, int V)
    {
        Console.WriteLine("Shortest distances between every pair of vertices:");
        for (int i = 0; i < V; i++)
        {
            for (int j = 0; j < V; j++)
            {
                if (dist[i, j] == int.MaxValue)
                    Console.Write("INF ");
                else
                    Console.Write(dist[i, j] + " ");
            }
            Console.WriteLine();
        }
    }
}
```

---

## Time and Space Complexity

**Time Complexity**

- O(V³), where V is the number of vertices.

**Space Complexity**

- O(V²), for the distance matrix.

---

## Uses

- All-pairs shortest path in graphs
- Network routing
- Transitive closure
- Detecting negative cycles (if `dist[i][i] < 0` for
