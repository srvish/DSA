# Queue Implementation in C#

## Algorithm Steps

- Initialize an array (or list) to store queue elements.
- Maintain two pointers: `front` and `rear`.
- **Enqueue (Add element):**
  - Check if the queue is full.
  - If not, increment `rear` and insert the element.
- **Dequeue (Remove element):**
  - Check if the queue is empty.
  - If not, increment `front` and return the element.
- **Peek (Front element):**
  - Return the element at `front` without removing it.
- **IsEmpty:**
  - Check if `front > rear`.

---

## C# Code Example

```csharp
// Simple Queue implementation using array
public class Queue
{
    private int[] items;
    private int front;
    private int rear;
    private int maxSize;

    public Queue(int size)
    {
        maxSize = size;
        items = new int[maxSize];
        front = 0;
        rear = -1;
    }

    public bool IsEmpty()
    {
        return front > rear;
    }

    public bool IsFull()
    {
        return rear == maxSize - 1;
    }

    public void Enqueue(int value)
    {
        if (IsFull())
        {
            throw new InvalidOperationException("Queue is full");
        }
        items[++rear] = value;
    }

    public int Dequeue()
    {
        if (IsEmpty())
        {
            throw new InvalidOperationException("Queue is empty");
        }
        return items[front++];
    }

    public int Peek()
    {
        if (IsEmpty())
        {
            throw new InvalidOperationException("Queue is empty");
        }
        return items[front];
    }
}
```

## Time and Space Complexity

**Time Complexity**

- **Enqueue:** O(1)
- **Dequeue:** O(1)
- **Peek:** O(1)

**Space Complexity:** O(n), where n is the size of the queue.
