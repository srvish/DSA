# Union-Find Algorithm (Disjoint Set Union - DSU)

The Union-Find algorithm, also known as Disjoint Set Union (DSU), is a data structure that keeps track of a set of elements partitioned into a number of disjoint (non-overlapping) subsets. It supports two main operations efficiently:

**Algorithm Steps:**

- **Find:** Determine which subset a particular element is in. This can be used for checking if two elements are in the same subset.
- **Union:** Join two subsets into a single subset.

**Optimizations:**

- **Path Compression:** Flattens the structure of the tree whenever Find is called, making future operations faster.
- **Union by Rank/Size:** Always attach the smaller tree to the root of the larger tree to keep the tree shallow.

**Applications:**

- Kruskal’s Minimum Spanning Tree algorithm
- Connected components in a graph
- Network connectivity
- Image processing (connected component labeling)

---

## C# Example (Union by Rank)

```csharp
public class UnionFind
{
    private int[] parent;
    private int[] rank;

    public UnionFind(int size)
    {
        parent = new int[size];
        rank = new int[size];
        for (int i = 0; i < size; i++) {
            parent[i] = i;
        }
    }

    // Find with path compression
    public int Find(int x)
    {
        if (parent[x] != x) {
            parent[x] = Find(parent[x]);
        }
        return parent[x];
    }

    // Union by rank
    public void Union(int x, int y)
    {
        int rootX = Find(x);
        int rootY = Find(y);
        if (rootX == rootY) {
            return;
        }

        if (rank[rootX] < rank[rootY]) {
            parent[rootX] = rootY;
        }
        else if (rank[rootX] > rank[rootY]) {
            parent[rootY] = rootX;
        }
        else {
            parent[rootY] = rootX;
            rank[rootX]++;
        }
    }
}
```

---

## C# Example (Union by Size)

```csharp
public class UnionFindBySize
{
    private int[] parent;
    private int[] size;

    public UnionFindBySize(int count)
    {
        parent = new int[count];
        size = new int[count];
        for (int i = 0; i < count; i++)
        {
            parent[i] = i;
            size[i] = 1; // Each component is initially of size 1
        }
    }

    // Find with path compression (remains the same)
    public int Find(int x)
    {
        if (parent[x] != x) {
            parent[x] = Find(parent[x]);
        }

        return parent[x];
    }

    // Union by size
    public void Union(int x, int y)
    {
        int rootX = Find(x);
        int rootY = Find(y);
        if (rootX == rootY) return;

        // Attach smaller tree to the root of the larger tree
        if (size[rootX] < size[rootY])
        {
            parent[rootX] = rootY;
            size[rootY] += size[rootX];
        }
        else
        {
            parent[rootY] = rootX;
            size[rootX] += size[rootY];
        }
    }
}
```

---

**Time Complexity:**

- Nearly O(1) per operation (amortized, using path compression and union by rank)

**Space Complexity:** O(N)
