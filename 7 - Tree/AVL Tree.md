# AVL Tree (Self-Balancing Binary Search Tree)

An AVL Tree is a self-balancing binary search tree where the difference between heights of left and right subtrees cannot be more than one for all nodes.

---

## Algorithm Steps

**Insertion:**

- Insert the node as in a regular BST.
- Update the height of the ancestor node.
- Get the balance factor (height of left subtree - height of right subtree).
- If the node becomes unbalanced, perform rotations:
  - Left Left Case: Right rotate.
  - Right Right Case: Left rotate.
  - Left Right Case: Left rotate left child, then right rotate.
  - Right Left Case: Right rotate right child, then left rotate.

**Rotation:**

- Right Rotation: Rotate the subtree to the right.
- Left Rotation: Rotate the subtree to the left.

---

## C# Implementation

```csharp
public class AVLNode
{
    public int val;
    public AVLNode left, right;
    public int height;
    public AVLNode(int x)
    {
        val = x;
        height = 1;
    }
}

public class AVLTree
{
    public AVLNode root;

    // Get height
    private int Height(AVLNode node) => node?.height ?? 0;

    // Get balance factor
    private int GetBalance(AVLNode node) => node == null ? 0 : Height(node.left) - Height(node.right);

    // Right rotate
    private AVLNode RightRotate(AVLNode y)
    {
        AVLNode x = y.left;
        AVLNode T2 = x.right;

        x.right = y;
        y.left = T2;

        y.height = Math.Max(Height(y.left), Height(y.right)) + 1;
        x.height = Math.Max(Height(x.left), Height(x.right)) + 1;

        return x;
    }

    // Left rotate
    private AVLNode LeftRotate(AVLNode x)
    {
        AVLNode y = x.right;
        AVLNode T2 = y.left;

        y.left = x;
        x.right = T2;

        x.height = Math.Max(Height(x.left), Height(x.right)) + 1;
        y.height = Math.Max(Height(y.left), Height(y.right)) + 1;

        return y;
    }

    // Insert
    public AVLNode Insert(AVLNode node, int key)
    {
        if (node == null)
            return new AVLNode(key);

        if (key < node.val)
            node.left = Insert(node.left, key);
        else if (key > node.val)
            node.right = Insert(node.right, key);
        else
            return node; // Duplicate keys not allowed

        node.height = 1 + Math.Max(Height(node.left), Height(node.right));
        int balance = GetBalance(node);

        // Left Left Case
        if (balance > 1 && key < node.left.val)
            return RightRotate(node);

        // Right Right Case
        if (balance < -1 && key > node.right.val)
            return LeftRotate(node);

        // Left Right Case
        if (balance > 1 && key > node.left.val)
        {
            node.left = LeftRotate(node.left);
            return RightRotate(node);
        }

        // Right Left Case
        if (balance < -1 && key < node.right.val)
        {
            node.right = RightRotate(node.right);
            return LeftRotate(node);
        }

        return node;
    }
}
```

---

**Time Complexity:** O(log N) for insert, delete, and search  
**Space Complexity:** O(log N) (due to recursion stack)
