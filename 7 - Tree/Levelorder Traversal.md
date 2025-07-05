# Level Order Traversal (Binary Tree)

Level order traversal visits the nodes of a binary tree level by level from left to right.

**Algorithm Steps:**

- Initialize an empty queue and enqueue the root node.
- While the queue is not empty:
  - Dequeue a node from the queue and visit it.
  - Enqueue the left child of the node (if any).
  - Enqueue the right child of the node (if any).

---

## Level Order Traversal (C#)

```csharp
public class TreeNode
{
    public int val;
    public TreeNode left, right;
    public TreeNode(int x) { val = x; }
}

public void LevelOrder(TreeNode root)
{
    if (root == null)
        return;

    Queue<TreeNode> queue = new Queue<TreeNode>();
    queue.Enqueue(root);

    while (queue.Count > 0)
    {
        TreeNode node = queue.Dequeue();
        Console.Write(node.val + " ");

        if (node.left != null)
            queue.Enqueue(node.left);
        if (node.right != null)
            queue.Enqueue(node.right);
    }
}
```

---

**Time Complexity:** O(N)  
**Space Complexity:** O(N)
