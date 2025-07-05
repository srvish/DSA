# Inorder Traversal (Binary Tree)

Inorder traversal visits the nodes of a binary tree in the following order: **Left subtree → Root → Right subtree**.

**Algorithm Steps (Recursive):**

- Traverse the left subtree.
- Visit the root node.
- Traverse the right subtree.

---

## Recursive Inorder Traversal (C#)

```csharp
public class TreeNode
{
    public int val;
    public TreeNode left, right;
    public TreeNode(int x) { val = x; }
}

public void InorderRecursive(TreeNode root)
{
    if (root == null)
        return;
    InorderRecursive(root.left);
    Console.Write(root.val + " ");
    InorderRecursive(root.right);
}
```

**Algorithm Steps (Iterative):**

- Initialize an empty stack and set the current node to the root.
- While the current node is not null or the stack is not empty:
  - Traverse to the leftmost node, pushing nodes onto the stack.
  - Pop a node from the stack, visit it, and set current to its right child.

---

## Iterative Inorder Traversal (C#)

```csharp
public void InorderIterative(TreeNode root)
{
    Stack<TreeNode> stack = new Stack<TreeNode>();
    TreeNode current = root;

    while (current != null || stack.Count > 0)
    {
        while (current != null)
        {
            stack.Push(current);
            current = current.left;
        }
        current = stack.Pop();
        Console.Write(current.val + " ");
        current = current.right;
    }
}
```

---

**Time Complexity:** O(N)  
**Space Complexity:** O(N) (due to recursion stack or explicit stack)
