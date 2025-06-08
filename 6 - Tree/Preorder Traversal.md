# Preorder Traversal (Binary Tree)

Preorder traversal visits the nodes of a binary tree in the following order: **Root → Left subtree → Right subtree**.

**Algorithm Steps (Recursive):**

- Visit the root node.
- Traverse the left subtree.
- Traverse the right subtree.

---

## Recursive Preorder Traversal (C#)

```csharp
public class TreeNode
{
    public int val;
    public TreeNode left, right;
    public TreeNode(int x) { val = x; }
}

public void PreorderRecursive(TreeNode root)
{
    if (root == null)
        return;
    Console.Write(root.val + " ");
    PreorderRecursive(root.left);
    PreorderRecursive(root.right);
}
```

**Algorithm Steps (Iterative):**

- Initialize an empty stack and push the root node onto the stack.
- While the stack is not empty:
  - Pop a node from the stack and visit it.
  - Push the right child (if any) onto the stack.
  - Push the left child (if any) onto the stack.

---

## Iterative Preorder Traversal (C#)

```csharp
public void PreorderIterative(TreeNode root)
{
    if (root == null)
        return;

    Stack<TreeNode> stack = new Stack<TreeNode>();
    stack.Push(root);

    while (stack.Count > 0)
    {
        TreeNode node = stack.Pop();
        Console.Write(node.val + " ");

        if (node.right != null)
            stack.Push(node.right);
        if (node.left != null)
            stack.Push(node.left);
    }
}
```

---

**Time Complexity:** O(N)  
**Space Complexity:** O(N) (due to recursion stack or explicit stack)
