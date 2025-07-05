# B-Tree

A B-Tree is a self-balancing search tree in which nodes can have more than two children. It is commonly used in databases and file systems for efficient storage and retrieval.

---

## Algorithm Steps

**Insertion:**

- Start from the root and find the appropriate leaf node where the key should be inserted.
- If the leaf node is not full, insert the key in sorted order.
- If the leaf node is full, split the node:
  - Move the median key up to the parent.
  - Split the node into two nodes.
  - If the parent is also full, repeat the split process up the tree.
- If the root is full, create a new root and split the old root.

**Search:**

- Start from the root and compare the key with the keys in the current node.
- If the key is found, return true.
- If the key is less than a key in the node, move to the left child; if greater, move to the right child.
- Repeat until the key is found or a leaf node is reached.

---

## C# Implementation (for order t B-Tree)

```csharp
public class BTreeNode
{
    public int[] keys;
    public int t; // Minimum degree
    public BTreeNode[] children;
    public int n; // Current number of keys
    public bool leaf;

    public BTreeNode(int t, bool leaf)
    {
        this.t = t;
        this.leaf = leaf;
        keys = new int[2 * t - 1];
        children = new BTreeNode[2 * t];
        n = 0;
    }

    // Search key in subtree rooted with this node
    public BTreeNode Search(int key)
    {
        int i = 0;
        while (i < n && key > keys[i])
            i++;
        if (i < n && keys[i] == key)
            return this;
        if (leaf)
            return null;
        return children[i].Search(key);
    }

    // Insert a new key in the subtree rooted with this node
    public void InsertNonFull(int key)
    {
        int i = n - 1;
        if (leaf)
        {
            while (i >= 0 && keys[i] > key)
            {
                keys[i + 1] = keys[i];
                i--;
            }
            keys[i + 1] = key;
            n++;
        }
        else
        {
            while (i >= 0 && keys[i] > key)
                i--;
            if (children[i + 1].n == 2 * t - 1)
            {
                SplitChild(i + 1, children[i + 1]);
                if (keys[i + 1] < key)
                    i++;
            }
            children[i + 1].InsertNonFull(key);
        }
    }

    // Split the child y of this node. i is index of y in child array
    public void SplitChild(int i, BTreeNode y)
    {
        BTreeNode z = new BTreeNode(y.t, y.leaf);
        z.n = t - 1;
        for (int j = 0; j < t - 1; j++)
            z.keys[j] = y.keys[j + t];
        if (!y.leaf)
        {
            for (int j = 0; j < t; j++)
                z.children[j] = y.children[j + t];
        }
        y.n = t - 1;
        for (int j = n; j >= i + 1; j--)
            children[j + 1] = children[j];
        children[i + 1] = z;
        for (int j = n - 1; j >= i; j--)
            keys[j + 1] = keys[j];
        keys[i] = y.keys[t - 1];
        n++;
    }
}

public class BTree
{
    public BTreeNode root;
    public int t; // Minimum degree

    public BTree(int t)
    {
        this.t = t;
        root = null;
    }

    public void Insert(int key)
    {
        if (root == null)
        {
            root = new BTreeNode(t, true);
            root.keys[0] = key;
            root.n = 1;
        }
        else
        {
            if (root.n == 2 * t - 1)
            {
                BTreeNode s = new BTreeNode(t, false);
                s.children[0] = root;
                s.SplitChild(0, root);
                int i = 0;
                if (s.keys[0] < key)
                    i++;
                s.children[i].InsertNonFull(key);
                root = s;
            }
            else
            {
                root.InsertNonFull(key);
            }
        }
    }

    public bool Search(int key)
    {
        return root != null && root.Search(key) != null;
    }
}
```

---

**Time Complexity:**

- Search: O(log N)
- Insert: O(log N)
- Delete: O(log N) (not included above, but similar complexity)

**Space Complexity:** O(N)
