# Prim's Algorithm (Minimum Spanning Tree) Implementation in C#

## Algorithm Steps

- Represent the graph using an adjacency matrix.
- Create arrays to track the minimum edge weight to each vertex (`key`), the parent of each vertex in the MST (`parent`), and whether a vertex is included in the MST (`mstSet`).
- Initialize all `key` values as infinity except for the first vertex, which is set to 0.
- For each vertex:
  - Pick the vertex not yet included in MST with the minimum `key` value.
  - Include this vertex in the MST set.
  - Update the `key` and `parent` values of its adjacent vertices if a smaller edge is found.

---

## C# Code Example (Adjacency Matrix)

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

- O(V²), for

## Uses

Prim's algorithm is primarily used to find the Minimum Spanning Tree (MST) of a connected, weighted, undirected graph. Besides constructing MSTs, it is also used for:

- **Network Design:** Designing least-cost networks such as computer, telecommunication, electrical, and road networks.
- **Approximation Algorithms:** As a subroutine in algorithms for problems like the Traveling Salesman Problem (TSP) and clustering.
- **Reducing Redundancy:** Removing redundant connections in a network while maintaining connectivity.
- **Image Processing:** In segmentation and constructing region adjacency graphs.
- **Circuit Design:** Laying out wiring with minimal total length in VLSI design.
