# Red-Black Tree

A Red-Black Tree is a self-balancing binary search tree where each node contains an extra bit for denoting the color of the node, either red or black. It ensures the tree remains approximately balanced, guaranteeing O(log N) time for search, insert, and delete operations.

---

## Algorithm Steps

**Properties:**

- Every node is either red or black.
- The root is always black.
- All leaves (null nodes) are black.
- If a node is red, both its children are black (no two reds in a row).
- Every path from a node to its descendant leaves contains the same number of black nodes.

**Insertion:**

- Insert the node as in a regular BST and color it red.
- Fix any violations of the Red-Black properties by:
  - Recoloring nodes.
  - Performing left or right rotations as needed.
- Ensure the root is always black.

**Deletion:**

- Remove the node as in a regular BST.
- If the removed node or its replacement is black, fix any violations by:
  - Recoloring nodes.
  - Performing rotations as needed.
- Ensure the root is always black.

---

## C# Implementation (Simplified)

```csharp
public enum Color { Red, Black }

public class RBNode
{
    public int val;
    public Color color;
    public RBNode left, right, parent;

    public RBNode(int val)
    {
        this.val = val;
        color = Color.Red;
        left = right = parent = null;
    }
}

public class RedBlackTree
{
    private RBNode root;

    // Left rotate
    private void LeftRotate(RBNode x)
    {
        RBNode y = x.right;
        x.right = y.left;
        if (y.left != null)
            y.left.parent = x;
        y.parent = x.parent;
        if (x.parent == null)
            root = y;
        else if (x == x.parent.left)
            x.parent.left = y;
        else
            x.parent.right = y;
        y.left = x;
        x.parent = y;
    }

    // Right rotate
    private void RightRotate(RBNode y)
    {
        RBNode x = y.left;
        y.left = x.right;
        if (x.right != null)
            x.right.parent = y;
        x.parent = y.parent;
        if (y.parent == null)
            root = x;
        else if (y == y.parent.left)
            y.parent.left = x;
        else
            y.parent.right = x;
        x.right = y;
        y.parent = x;
    }

    // Insert
    public void Insert(int key)
    {
        RBNode node = new RBNode(key);
        RBNode y = null;
        RBNode x = root;

        while (x != null)
        {
            y = x;
            if (node.val < x.val)
                x = x.left;
            else
                x = x.right;
        }
        node.parent = y;
        if (y == null)
            root = node;
        else if (node.val < y.val)
            y.left = node;
        else
            y.right = node;

        node.left = node.right = null;
        node.color = Color.Red;

        InsertFixup(node);
    }

    // Fix Red-Black Tree after insertion
    private void InsertFixup(RBNode z)
    {
        while (z.parent != null && z.parent.color == Color.Red)
        {
            if (z.parent == z.parent.parent.left)
            {
                RBNode y = z.parent.parent.right;
                if (y != null && y.color == Color.Red)
                {
                    z.parent.color = Color.Black;
                    y.color = Color.Black;
                    z.parent.parent.color = Color.Red;
                    z = z.parent.parent;
                }
                else
                {
                    if (z == z.parent.right)
                    {
                        z = z.parent;
                        LeftRotate(z);
                    }
                    z.parent.color = Color.Black;
                    z.parent.parent.color = Color.Red;
                    RightRotate(z.parent.parent);
                }
            }
            else
            {
                RBNode y = z.parent.parent.left;
                if (y != null && y.color == Color.Red)
                {
                    z.parent.color = Color.Black;
                    y.color = Color.Black;
                    z.parent.parent.color = Color.Red;
                    z = z.parent.parent;
                }
                else
                {
                    if (z == z.parent.left)
                    {
                        z = z.parent;
                        RightRotate(z);
                    }
                    z.parent.color = Color.Black;
                    z.parent.parent.color = Color.Red;
                    LeftRotate(z.parent.parent);
                }
            }
        }
        root.color = Color.Black;
    }

    // Search
    public RBNode Search(int key)
    {
        RBNode current = root;
        while (current != null)
        {
            if (key == current.val)
                return current;
            else if (key < current.val)
                current = current.left;
            else
                current = current.right;
        }
        return null;
    }
}
```

---

**Time Complexity:**

- Search: O(log N)
- Insert: O(log N)
- Delete: O(log N)

**Space Complexity:** O(log N) (due to recursion stack or tree height)
