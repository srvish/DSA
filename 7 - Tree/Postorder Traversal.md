# Postorder Traversal (Binary Tree)

Postorder traversal visits the nodes of a binary tree in the following order: **Left subtree → Right subtree → Root**.

**Algorithm Steps (Recursive):**

- Traverse the left subtree.
- Traverse the right subtree.
- Visit the root node.

---

## Recursive Postorder Traversal (C#)

```csharp
public class TreeNode
{
    public int val;
    public TreeNode left, right;
    public TreeNode(int x) { val = x; }
}

public void PostorderRecursive(TreeNode root)
{
    if (root == null)
        return;
    PostorderRecursive(root.left);
    PostorderRecursive(root.right);
    Console.Write(root.val + " ");
}
```

**Algorithm Steps (Iterative):**

- Initialize two stacks: `stack1` and `stack2`.
- Push the root node onto `stack1`.
- While `stack1` is not empty:
  - Pop a node from `stack1` and push it onto `stack2`.
  - Push the left child (if any) onto `stack1`.
  - Push the right child (if any) onto `stack1`.
- After the loop, pop all nodes from `stack2` and visit them.

---

## Iterative Postorder Traversal (C#) - One way

```csharp
public void PostorderIterative(TreeNode root)
{
    if (root == null)
        return;

    Stack<TreeNode> stack1 = new Stack<TreeNode>();
    Stack<TreeNode> stack2 = new Stack<TreeNode>();
    stack1.Push(root);

    while (stack1.Count > 0)
    {
        TreeNode node = stack1.Pop();
        stack2.Push(node);

        if (node.left != null)
            stack1.Push(node.left);
        if (node.right != null)
            stack1.Push(node.right);
    }

    while (stack2.Count > 0)
    {
        Console.Write(stack2.Pop().val + " ");
    }
}
```

## Iterative Postorder Traversal (C#) - Another way

```csharp
public void PostorderIterative(TreeNode root)
{
    if (root == null)
        return;

    Stack<TreeNode> stack1 = new Stack<TreeNode>();
    Stack<TreeNode> stack2 = new Stack<TreeNode>();
    stack1.Push(root);

    while (stack1.Count > 0)
    {
        TreeNode node = stack1.Pop();
        stack2.Push(node);

        if (node.left != null)
            stack1.Push(node.left);
        if (node.right != null)
            stack1.Push(node.right);
    }

    while (stack2.Count > 0)
    {
        Console.Write(stack2.Pop().val + " ");
    }
}
```

---

**Time Complexity:** O(N)  
**Space Complexity:** O(N) (due to recursion stack or explicit stacks)
