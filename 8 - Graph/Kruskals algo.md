# Kruskal's Algorithm (Minimum Spanning Tree) Implementation in C#

## Algorithm Steps

- Represent the graph as a list of edges (each edge has a source, destination, and weight).
- Sort all edges in non-decreasing order of their weight.
- Initialize a parent array for union-find to detect cycles.
- For each edge in the sorted list:
  - If including the edge does not form a cycle (i.e., the source and destination are in different sets):
    - Add the edge to the MST.
    - Union the sets of the source and destination.
- Repeat until the MST contains (V - 1) edges, where V is the number of vertices.

---

## C# Code Example (Edge List)

```csharp
using System;
using System.Collections.Generic;

public class KruskalMST
{
    public class Edge : IComparable<Edge>
    {
        public int Src, Dest, Weight;
        public int CompareTo(Edge other)
        {
            return this.Weight.CompareTo(other.Weight);
        }
    }

    private int vertices;
    private List<Edge> edges = new List<Edge>();

    public KruskalMST(int v)
    {
        vertices = v;
    }

    public void AddEdge(int src, int dest, int weight)
    {
        edges.Add(new Edge { Src = src, Dest = dest, Weight = weight });
    }

    // Find set of an element i (uses path compression)
    private int Find(int[] parent, int i)
    {
        if (parent[i] != i)
            parent[i] = Find(parent, parent[i]);
        return parent[i];
    }

    // Union of two sets x and y (uses union by rank)
    private void Union(int[] parent, int[] rank, int x, int y)
    {
        int xroot = Find(parent, x);
        int yroot = Find(parent, y);

        if (rank[xroot] < rank[yroot])
            parent[xroot] = yroot;
        else if (rank[xroot] > rank[yroot])
            parent[yroot] = xroot;
        else
        {
            parent[yroot] = xroot;
            rank[xroot]++;
        }
    }

    public void Kruskal()
    {
        List<Edge> result = new List<Edge>();
        edges.Sort();

        int[] parent = new int[vertices];
        int[] rank = new int[vertices];

        for (int v = 0; v < vertices; v++)
        {
            parent[v] = v;
            rank[v] = 0;
        }

        int e = 0, i = 0;
        while (e < vertices - 1 && i < edges.Count)
        {
            Edge nextEdge = edges[i++];
            int x = Find(parent, nextEdge.Src);
            int y = Find(parent, nextEdge.Dest);

            if (x != y)
            {
                result.Add(nextEdge);
                Union(parent, rank, x, y);
                e++;
            }
        }

        Console.WriteLine("Edge \tWeight");
        foreach (var edge in result)
            Console.WriteLine($"{edge.Src} - {edge.Dest}\t{edge.Weight}");
    }
}
```

---

## Time and Space Complexity

**Time Complexity**

- O(E log E), where E is the number of edges (due to sorting).

**Space Complexity**

- O(V + E), for storing parent, rank arrays, and the edge list.

## Uses

Kruskal's algorithm is used for:

- **Network Design:** Finding the least-cost network in computer, telecommunication, and transportation networks.
- **Clustering:** As a subroutine in clustering algorithms.
- **Approximation Algorithms:** For problems like the Traveling Salesman Problem (TSP).
- **Reducing Redundancy:** Removing unnecessary connections while maintaining connectivity.
