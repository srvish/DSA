# Binary Search Tree (BST) - Search, Insert, and Delete

A Binary Search Tree is a binary tree in which each node has a comparable key (and associated value) and satisfies the property that the key in each node is:

- Greater than all keys in its left subtree
- Less than all keys in its right subtree

---

## Algorithm Steps

**Search:**

- Start at the root.
- If the key matches the root, return the node.
- If the key is less, search the left subtree.
- If the key is greater, search the right subtree.
- Repeat until the key is found or the subtree is null.

**Insert:**

- Start at the root.
- If the tree is empty, insert the new node as root.
- If the key is less than the current node, insert in the left subtree.
- If the key is greater, insert in the right subtree.
- Repeat until the correct null position is found.

**Delete:**

- Search for the node to delete.
- If the node has no children, simply remove it.
- If the node has one child, replace the node with its child.
- If the node has two children:
  - Find the inorder successor (smallest in the right subtree).
  - Replace the node's value with the successor's value.
  - Delete the inorder successor.

---

## C# Implementation

```csharp
public class TreeNode
{
    public int val;
    public TreeNode left, right;
    public TreeNode(int x) { val = x; }
}

public class BST
{
    public TreeNode root;

    // Search
    public TreeNode Search(TreeNode node, int key)
    {
        if (node == null || node.val == key)
            return node;
        if (key < node.val)
            return Search(node.left, key);
        else
            return Search(node.right, key);
    }

    // Insert
    public TreeNode Insert(TreeNode node, int key)
    {
        if (node == null)
            return new TreeNode(key);
        if (key < node.val)
            node.left = Insert(node.left, key);
        else if (key > node.val)
            node.right = Insert(node.right, key);
        // If key == node.val, do nothing (no duplicates)
        return node;
    }

    // Delete
    public TreeNode Delete(TreeNode node, int key)
    {
        if (node == null)
            return null;
        if (key < node.val)
            node.left = Delete(node.left, key);
        else if (key > node.val)
            node.right = Delete(node.right, key);
        else
        {
            // Node with only one child or no child
            if (node.left == null)
                return node.right;
            else if (node.right == null)
                return node.left;

            // Node with two children: Get inorder successor (smallest in the right subtree)
            node.val = MinValue(node.right);
            node.right = Delete(node.right, node.val);
        }
        return node;
    }

    private int MinValue(TreeNode node)
    {
        int minv = node.val;
        while (node.left != null)
        {
            minv = node.left.val;
            node = node.left;
        }
        return minv;
    }
}
```

---

**Time Complexity:**

- Search: O(h)
- Insert: O(h)
- Delete: O(h)  
  Where h is the height of the tree (O(log N) for balanced BST, O(N) for skewed BST).

**Space Complexity:** O(h) (due to recursion stack)
