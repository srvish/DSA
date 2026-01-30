# Topological Sort Algorithm (Directed Acyclic Graph) Implementation in C#

## Algorithm Steps

- video link https://youtu.be/cIBFEhD77b4
- problem: https://leetcode.com/problems/course-schedule/description/?envType=problem-list-v2&envId=xr3pqjki
- Represent the graph using an adjacency list.
- Maintain a boolean array to mark visited nodes.
- Use a stack to store the topological order.
- For each unvisited node, perform DFS:
  - Mark the node as visited.
  - Recursively visit all its unvisited neighbors.
  - After visiting all neighbors, push the node onto the stack.
- After all nodes are processed, pop elements from the stack to get the topological order.

---

## C# Code Example (Adjacency List)

```csharp
using System;
using System.Collections.Generic;

public class TopologicalSort
{
    private int vertices;
    private List<int>[] adjList;

    public TopologicalSort(int v)
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

    private void TopoSortUtil(int v, bool[] visited, Stack<int> stack)
    {
        visited[v] = true;
        foreach (int neighbor in adjList[v])
        {
            if (!visited[neighbor])
                TopoSortUtil(neighbor, visited, stack);
        }
        stack.Push(v);
    }

    public void TopologicalSortAlgo()
    {
        Stack<int> stack = new Stack<int>();
        bool[] visited = new bool[vertices];

        for (int i = 0; i < vertices; i++)
            if (!visited[i])
                TopoSortUtil(i, visited, stack);

        Console.WriteLine("Topological Order:");
        while (stack.Count > 0)
            Console.Write(stack.Pop() + " ");
        Console.WriteLine();
    }
}
```

---

## Time and Space Complexity

**Time Complexity**

- O(V + E), where V is the number of vertices and E is the number of edges.

**Space Complexity**

- O(V + E), for the adjacency list, visited array, and stack.

## Uses

Topological sort is used for:

- **Task scheduling** (e.g., course prerequisites, build systems).
- **Dependency resolution** in package managers.
- **Instruction scheduling** in compilers.
- **Finding orderings**
