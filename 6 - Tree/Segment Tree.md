# Segment Tree

A Segment Tree is a binary tree used for storing intervals or segments. It allows querying and updating ranges efficiently, such as finding the sum or minimum in a range.

---

## Algorithm Steps

**Build:**

- Recursively divide the array into two halves.
- Store the result (e.g., sum, min, max) for each segment in a tree node.
- Continue until each leaf node represents a single element.

**Query (Range Query):**

- If the query range matches the node range, return the node value.
- If the query range is outside the node range, return a neutral value (e.g., 0 for sum, infinity for min).
- Otherwise, split the query into left and right children and combine their results.

**Update:**

- Update the value at a specific index.
- Recursively update the affected nodes up the tree.

---

## C# Implementation (for Range Sum Query)

```csharp
public class SegmentTree
{
    private int[] tree;
    private int n;

    public SegmentTree(int[] arr)
    {
        n = arr.Length;
        tree = new int[4 * n];
        Build(arr, 0, n - 1, 1);
    }

    private void Build(int[] arr, int l, int r, int idx)
    {
        if (l == r)
        {
            tree[idx] = arr[l];
            return;
        }
        int mid = (l + r) / 2;
        Build(arr, l, mid, 2 * idx);
        Build(arr, mid + 1, r, 2 * idx + 1);
        tree[idx] = tree[2 * idx] + tree[2 * idx + 1];
    }

    // Range sum query
    public int Query(int ql, int qr)
    {
        return Query(1, 0, n - 1, ql, qr);
    }

    private int Query(int idx, int l, int r, int ql, int qr)
    {
        if (ql > r || qr < l)
            return 0; // Out of range
        if (ql <= l && r <= qr)
            return tree[idx]; // Complete overlap
        int mid = (l + r) / 2;
        return Query(2 * idx, l, mid, ql, qr) + Query(2 * idx + 1, mid + 1, r, ql, qr);
    }

    // Point update
    public void Update(int pos, int val)
    {
        Update(1, 0, n - 1, pos, val);
    }

    private void Update(int idx, int l, int r, int pos, int val)
    {
        if (l == r)
        {
            tree[idx] = val;
            return;
        }
        int mid = (l + r) / 2;
        if (pos <= mid)
            Update(2 * idx, l, mid, pos, val);
        else
            Update(2 * idx + 1, mid + 1, r, pos, val);
        tree[idx] = tree[2 * idx] + tree[2 * idx + 1];
    }
}
```

---

**Time Complexity:**

- Build: O(N)
- Query: O(log N)
- Update: O(log N)

**Space Complexity:** O(N)
