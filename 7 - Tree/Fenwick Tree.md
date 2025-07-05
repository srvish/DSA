# Fenwick Tree (Binary Indexed Tree)

A Fenwick Tree, also known as a Binary Indexed Tree (BIT), is a data structure that provides efficient methods for calculation and manipulation of prefix sums in a table of values.

---

## Algorithm Steps

**Build:**

- Initialize an array (tree) of size N+1 (1-based indexing).
- For each index, update the tree with the value at that index.

**Update:**

- To add a value to an element, update the tree at the index and all relevant ancestors by moving to the next index using `index += index & -index`.

**Query (Prefix Sum):**

- To get the prefix sum up to a given index, sum the values at the index and all relevant ancestors by moving to the parent using `index -= index & -index`.

---

## C# Implementation

```csharp
public class FenwickTree
{
    private int[] tree;
    private int n;

    public FenwickTree(int size)
    {
        n = size;
        tree = new int[n + 1];
    }

    // Add value to index (1-based)
    public void Update(int index, int value)
    {
        while (index <= n)
        {
            tree[index] += value;
            index += index & -index;
        }
    }

    // Get prefix sum up to index (1-based)
    public int Query(int index)
    {
        int sum = 0;
        while (index > 0)
        {
            sum += tree[index];
            index -= index & -index;
        }
        return sum;
    }

    // Get sum in range [left, right] (1-based)
    public int RangeQuery(int left, int right)
    {
        return Query(right) - Query(left - 1);
    }
}
```

---

**Time Complexity:**

- Build: O(N) (if built with repeated updates)
- Update: O(log N)
- Query: O(log N)

**Space Complexity:** O(N)
