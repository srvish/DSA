# Linked List Implementation in C#

## Algorithm Steps

- Define a `Node` class with `data` and `next` pointer.
- Maintain a reference to the `head` of the list.
- **Insert at end:**
  - Create a new node.
  - If the list is empty, set `head` to new node.
  - Else, traverse to the last node and set its `next` to new node.
- **Delete by value:**
  - Traverse the list to find the node with the given value.
  - Update the previous node's `next` to skip the deleted node.
- **Search for a value:**
  - Traverse the list and compare each node's data with the target value.
- **Display the list:**
  - Traverse from `head` and print each node's data.

---

## C# Code Example

```csharp
// Simple singly linked list implementation in C#
public class LinkedList
{
    public class Node
    {
        public int data;
        public Node next;
        public Node(int value)
        {
            data = value;
            next = null;
        }
    }

    private Node head;

    // Insert at end
    public void Insert(int value)
    {
        Node newNode = new Node(value);
        if (head == null)
        {
            head = newNode;
            return;
        }
        Node current = head;
        while (current.next != null)
        {
            current = current.next;
        }
        current.next = newNode;
    }

    // Delete by value
    public void Delete(int value)
    {
        if (head == null) return;
        if (head.data == value)
        {
            head = head.next;
            return;
        }
        Node current = head;
        while (current.next != null && current.next.data != value)
        {
            current = current.next;
        }
        if (current.next != null)
        {
            current.next = current.next.next;
        }
    }

    // Search for a value
    public bool Search(int value)
    {
        Node current = head;
        while (current != null)
        {
            if (current.data == value)
                return true;
            current = current.next;
        }
        return false;
    }

    // Display the list
    public void Display()
    {
        Node current = head;
        while (current != null)
        {
            Console.Write(current.data + " ");
            current = current.next;
        }
        Console.WriteLine();
    }
}
```

## Time and Space Complexity

**Time Complexity**

- **Insert at end**: O(n)
- **Delete by value**: O(n)
- **Search**: O(n)
- **Display**: O(n)

**Space Complexity**: O(n), where n is the number of nodes in the list.
