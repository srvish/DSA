# Circular Queue Implementation in C#

## Algorithm Steps

- Initialize an array to store queue elements.
- Maintain two pointers: `front` and `rear`.
- **Enqueue (Add element):**
  - Check if the queue is full (`(rear + 1) % maxSize == front`).
  - If not, increment `rear` circularly and insert the element.
- **Dequeue (Remove element):**
  - Check if the queue is empty (`front == rear`).
  - If not, increment `front` circularly and return the element.
- **Peek (Front element):**
  - Return the element at `front` without removing it.
- **IsEmpty:**
  - Check if `front == rear`.
- **IsFull:**
  - Check if `(rear + 1) % maxSize == front`.

---

## C# Code Example

```csharp
// Circular Queue implementation using array
public class CircularQueue
{
    private int[] items;
    private int front;
    private int rear;
    private int maxSize;

    public CircularQueue(int size)
    {
        maxSize = size + 1; // One slot is used to distinguish full/empty
        items = new int[maxSize];
        front = 0;
        rear = 0;
    }

    public bool IsEmpty()
    {
        return front == rear;
    }

    public bool IsFull()
    {
        return (rear + 1) % maxSize == front;
    }

    public void Enqueue(int value)
    {
        if (IsFull())
            throw new InvalidOperationException("Queue is full");
        items[rear] = value;
        rear = (rear + 1) % maxSize;
    }

    public int Dequeue()
    {
        if (IsEmpty())
            throw new InvalidOperationException("Queue is empty");
        int value = items[front];
        front = (front + 1) % maxSize;
        return value;
    }

    public int Peek()
    {
        if (IsEmpty())
            throw new InvalidOperationException("Queue is empty");
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
