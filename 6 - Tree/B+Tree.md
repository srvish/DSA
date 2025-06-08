# B+ Tree

A B+ Tree is a self-balancing tree data structure that maintains sorted data and allows searches, sequential access, insertions, and deletions in logarithmic time. In a B+ Tree, all values are stored at the leaf level, and internal nodes only store keys for navigation.

---

## Algorithm Steps

**Insertion:**

- Start from the root and find the appropriate leaf node where the key should be inserted.
- Insert the key in sorted order in the leaf node.
- If the leaf node overflows (exceeds the maximum number of keys), split the node:
  - Move the middle key up to the parent node.
  - If the parent node also overflows, repeat the split process up the tree.
- If the root overflows, create a new root and split the old root.

**Search:**

- Start from the root and traverse down to the leaf node using the keys in internal nodes.
- Once at the leaf node, perform a linear search for the key.

**Note:**

- All leaf nodes are linked together for fast sequential access.

---

## C# Implementation (Simplified, Order t B+ Tree)

```csharp
public class BPlusTreeNode
{
    public int[] keys;
    public int t; // Minimum degree
    public BPlusTreeNode[] children;
    public int n; // Current number of keys
    public bool leaf;
    public BPlusTreeNode next; // Pointer to next leaf

    public BPlusTreeNode(int t, bool leaf)
    {
        this.t = t;
        this.leaf = leaf;
        keys = new int[2 * t - 1];
        children = new BPlusTreeNode[2 * t];
        n = 0;
        next = null;
    }
}

public class BPlusTree
{
    public BPlusTreeNode root;
    public int t; // Minimum degree

    public BPlusTree(int t)
    {
        this.t = t;
        root = null;
    }

    // Search for a key
    public bool Search(int key)
    {
        BPlusTreeNode node = root;
        while (node != null)
        {
            int i = 0;
            while (i < node.n && key > node.keys[i])
                i++;
            if (node.leaf)
            {
                if (i < node.n && node.keys[i] == key)
                    return true;
                return false;
            }
            node = node.children[i];
        }
        return false;
    }

    // Insert a key
    public void Insert(int key)
    {
        if (root == null)
        {
            root = new BPlusTreeNode(t, true);
            root.keys[0] = key;
            root.n = 1;
            return;
        }

        if (root.n == 2 * t - 1)
        {
            BPlusTreeNode s = new BPlusTreeNode(t, false);
            s.children[0] = root;
            SplitChild(s, 0, root);
            InsertNonFull(s, key);
            root = s;
        }
        else
        {
            InsertNonFull(root, key);
        }
    }

    private void InsertNonFull(BPlusTreeNode node, int key)
    {
        int i = node.n - 1;
        if (node.leaf)
        {
            while (i >= 0 && node.keys[i] > key)
            {
                node.keys[i + 1] = node.keys[i];
                i--;
            }
            node.keys[i + 1] = key;
            node.n++;
        }
        else
        {
            while (i >= 0 && node.keys[i] > key)
                i--;
            i++;
            if (node.children[i].n == 2 * t - 1)
            {
                SplitChild(node, i, node.children[i]);
                if (key > node.keys[i])
                    i++;
            }
            InsertNonFull(node.children[i], key);
        }
    }

    private void SplitChild(BPlusTreeNode parent, int i, BPlusTreeNode y)
    {
        BPlusTreeNode z = new BPlusTreeNode(y.t, y.leaf);
        z.n = t - 1;

        for (int j = 0; j < t - 1; j++)
            z.keys[j] = y.keys[j + t];

        if (!y.leaf)
        {
            for (int j = 0; j < t; j++)
                z.children[j] = y.children[j + t];
        }
        else
        {
            z.next = y.next;
            y.next = z;
        }

        y.n = t - 1;

        for (int j = parent.n; j >= i + 1; j--)
            parent.children[j + 1] = parent.children[j];
        parent.children[i + 1] = z;

        for (int j = parent.n - 1; j >= i; j--)
            parent.keys[j + 1] = parent.keys[j];
        parent.keys[i] = y.keys[t - 1];
        parent.n++;
    }
}
```

---

**Time Complexity:**

- Search: O(log N)
- Insert: O(log N)
- Delete: O(log N) (not included above, but similar complexity)

**Space Complexity:** O(N)
