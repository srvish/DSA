# Minimum Spanning Tree (MST)

## What is MST?

A **Minimum Spanning Tree (MST)** is a subset of the edges of a connected, weighted, undirected graph that connects all the vertices together, without any cycles, and with the minimum possible total edge weight.

- **Spanning Tree:** A subgraph that is a tree and connects all the vertices together.
- **Minimum Spanning Tree:** The spanning tree with the smallest total edge weight.

**Applications:**

- Network design (telecommunications, computer, electrical)
- Approximation algorithms (e.g., TSP)
- Cluster analysis

---

## Algorithm Steps (Prim's Algorithm, Adjacency Matrix)

- Represent the graph using an adjacency matrix.
- Create arrays to track the minimum edge weight to each vertex (`key`), the parent of each vertex in the MST (`parent`), and whether a vertex is included in the MST (`mstSet`).
- Initialize all `key` values as infinity except for the first vertex, which is set to 0.
- For each vertex:
  - Pick the vertex not yet included in MST with the minimum `key` value.
  - Include this vertex in the MST set.
  - Update the `key` and `parent` values of its adjacent vertices if a smaller edge is found.

---

## C# Code Example (Prim's Algorithm, Adjacency Matrix)

```csharp
using System;

public class PrimsMST
{
    private int vertices;

    public PrimsMST(int v)
    {
        vertices = v;
    }

    // Find the vertex with the minimum key value not yet included in MST
    private int MinKey(int[] key, bool[] mstSet)
    {
        int min = int.MaxValue, minIndex = -1;
        for (int v = 0; v < vertices; v++)
        {
            if (!mstSet[v] && key[v] < min)
            {
                min = key[v];
                minIndex = v;
            }
        }
        return minIndex;
    }

    // Print the constructed MST
    private void PrintMST(int[] parent, int[,] graph)
    {
        Console.WriteLine("Edge \tWeight");
        for (int i = 1; i < vertices; i++)
            Console.WriteLine($"{parent[i]} - {i}\t{graph[i, parent[i]]}");
    }

    public void PrimMST(int[,] graph)
    {
        int[] parent = new int[vertices]; // Array to store constructed MST
        int[] key = new int[vertices];    // Key values used to pick minimum weight edge
        bool[] mstSet = new bool[vertices]; // To represent set of vertices included in MST

        for (int i = 0; i < vertices; i++)
        {
            key[i] = int.MaxValue;
            mstSet[i] = false;
        }

        key[0] = 0;     // Start from the first vertex
        parent[0] = -1; // First node is always root of MST

        for (int count = 0; count < vertices - 1; count++)
        {
            int u = MinKey(key, mstSet);
            mstSet[u] = true;

            for (int v = 0; v < vertices; v++)
            {
                if (graph[u, v] != 0 && !mstSet[v] && graph[u, v] < key[v])
                {
                    parent[v] = u;
                    key[v] = graph[u, v];
                }
            }
        }

        PrintMST(parent, graph);
    }
}
```

---

## Time and Space Complexity

**Time Complexity**

- O(V²), where V is the number of vertices (for adjacency matrix implementation).

**Space Complexity**

- O(V²), for the adjacency matrix.

---

## Other MST Algorithms

- **Kruskal's Algorithm:** Greedy algorithm using edge list and union-find.
- **Boruvka's Algorithm:** Another greedy approach for MST.

Refer to [Prim’s](8%20-%20Graph/Prims%20algo.md) and [Kruskal’s](8%20-%20Graph/Kruskals%20algo.md) for more details.
