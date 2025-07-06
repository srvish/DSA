# Ford-Fulkerson Algorithm

## What is Ford-Fulkerson?

The **Ford-Fulkerson algorithm** is a greedy method for computing the maximum flow in a flow network. It repeatedly finds augmenting paths from the source to the sink and increases the flow along these paths until no more augmenting paths exist. The algorithm is the basis for the Edmonds-Karp algorithm (which uses BFS for finding shortest augmenting paths).

**Applications:**

- Network routing and bandwidth calculation
- Bipartite matching
- Project selection and scheduling
- Circulation with demands

---

## Algorithm Steps

- Initialize the flow in all edges to 0.
- While there exists an augmenting path from the source to the sink (using BFS or DFS):
  - Find the minimum residual capacity (bottleneck) along the path.
  - Augment the flow along the path by this bottleneck value.
  - Update the residual capacities of the edges and reverse edges along the path.
- Repeat until no more augmenting paths exist.

---

## C# Code Example

```csharp
using System;
using System.Collections.Generic;

public class FordFulkerson
{
    private int vertices;

    public FordFulkerson(int v)
    {
        vertices = v;
    }

    // BFS to find if there is a path from source to sink in residual graph
    private bool BFS(int[,] rGraph, int s, int t, int[] parent)
    {
        bool[] visited = new bool[vertices];
        Queue<int> queue = new Queue<int>();
        queue.Enqueue(s);
        visited[s] = true;
        parent[s] = -1;

        while (queue.Count > 0)
        {
            int u = queue.Dequeue();
            for (int v = 0; v < vertices; v++)
            {
                if (!visited[v] && rGraph[u, v] > 0)
                {
                    queue.Enqueue(v);
                    parent[v] = u;
                    visited[v] = true;
                }
            }
        }
        return visited[t];
    }

    // Returns the maximum flow from s to t in the given graph
    public int MaxFlow(int[,] graph, int s, int t)
    {
        int u, v;
        int[,] rGraph = new int[vertices, vertices];
        for (u = 0; u < vertices; u++)
            for (v = 0; v < vertices; v++)
                rGraph[u, v] = graph[u, v];

        int[] parent = new int[vertices];
        int maxFlow = 0;

        while (BFS(rGraph, s, t, parent))
        {
            int pathFlow = int.MaxValue;
            for (v = t; v != s; v = parent[v])
            {
                u = parent[v];
                pathFlow = Math.Min(pathFlow, rGraph[u, v]);
            }

            for (v = t; v != s; v = parent[v])
            {
                u = parent[v];
                rGraph[u, v] -= pathFlow;
                rGraph[v, u] += pathFlow;
            }

            maxFlow += pathFlow;
        }
        return maxFlow;
    }
}
```

---

## Time and Space Complexity

**Time Complexity**

- O(E \* max_flow), where E is the number of edges and max_flow is the maximum flow in the network.

**Space Complexity**

- O(V²), for the residual graph.

---

## Uses

- Network flow problems
- Bipartite matching
- Project selection and scheduling
-
