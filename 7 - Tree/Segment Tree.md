# Segment Tree

A Segment Tree is a binary tree used for storing intervals or segments. It allows querying and updating ranges efficiently, such as finding the sum or minimum or maximum in a range.

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
    // The array that stores the segment tree nodes
    private int[] tree;
    // The size of the input array
    private int n;

    // Constructor to build the segment tree from an input array
    public SegmentTree(int[] arr)
    {
        n = arr.Length;
        // The maximum size of a segment tree for an array of size n is approximately 4n
        tree = new int[4 * n];
        // Start the build process from the root of the tree (index 1)
        Build(arr, 0, n - 1, 1);
    }

    // Recursive function to build the segment tree
    // arr: input array, l: start index, r: end index, idx: current node index in the tree
    private void Build(int[] arr, int l, int r, int idx)
    {
        // Base case: if we are at a leaf node, store the element
        if (l == r)
        {
            tree[idx] = arr[l];
            return;
        }

        // Recursively build the left and right subtrees
        int mid = (l + r) / 2;
        // Left child will be at index 2*idx
        Build(arr, l, mid, 2 * idx);
        // Right child will be at index 2*idx + 1
        Build(arr, mid + 1, r, 2 * idx + 1);
        // Internal node will have the sum of its children
        tree[idx] = tree[2 * idx] + tree[2 * idx + 1];
    }

    // Range sum query
    // Public method to query the sum of a given range [ql, qr]
    public int Query(int ql, int qr)
    {
        // Start the query from the root of the tree (index 1)
        return Query(1, 0, n - 1, ql, qr);
    }

    // Recursive helper function for the query
    // idx: current node index, l/r: range of the current node, ql/qr: query range
    private int Query(int idx, int l, int r, int ql, int qr)
    {
        // Case 1: The current node's range is completely outside the query range
        if (ql > r || qr < l) {
            return 0; // Return 0 for sum, as it's the additive identity (out of range)
        }
        // Case 2: The current node's range is completely inside the query range
        if (ql <= l && r <= qr) {
            return tree[idx]; // Return the value of this node (complete overlap)
        }

        // Case 3: The current node's range partially overlaps with the query range
        // Recursively search in the left and right children and sum their results
        int mid = (l + r) / 2;
        return Query(2 * idx, l, mid, ql, qr) + Query(2 * idx + 1, mid + 1, r, ql, qr);
    }

    // Point update
    // Public method to update a value at a specific position in the original array
    public void Update(int pos, int val)
    {
        // Start the update from the root of the tree
        Update(1, 0, n - 1, pos, val);
    }

    // Recursive helper function to perform the update
    private void Update(int idx, int l, int r, int pos, int val)
    {
        // Base case: We've found the leaf node corresponding to the position to update
        if (l == r)
        {
            tree[idx] = val;
            return;
        }

        // If not at a leaf, go down the correct path (left or right)
        int mid = (l + r) / 2;
        if (pos <= mid) {
            Update(2 * idx, l, mid, pos, val); // Go left
        }
        else {
            Update(2 * idx + 1, mid + 1, r, pos, val); // Go right
        }

        // After the child node is updated, update the current node's value
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
