# Stack Implementation in C#

A **Stack** is a linear data structure that follows the Last-In-First-Out (LIFO) principle.

---

## Algorithm Steps

**Push:**

- Add the new element to the top of the stack.

**Pop:**

- Remove and return the top element from the stack.
- If the stack is empty, handle underflow.

**Peek/Top:**

- Return the top element without removing it.
- If the stack is empty, handle underflow.

**IsEmpty:**

- Check if the stack contains any elements.

---

## C# Implementation (using array)

```csharp
public class Stack
{
    private int[] arr;
    private int top;
    private int capacity;

    public Stack(int size)
    {
        arr = new int[size];
        capacity = size;
        top = -1;
    }

    // Push element onto stack
    public void Push(int x)
    {
        if (top == capacity - 1)
            throw new InvalidOperationException("Stack Overflow");
        arr[++top] = x;
    }

    // Pop element from stack
    public int Pop()
    {
        if (IsEmpty())
            throw new InvalidOperationException("Stack Underflow");
        return arr[top--];
    }

    // Peek at top element
    public int Peek()
    {
        if (IsEmpty())
            throw new InvalidOperationException("Stack is empty");
        return arr[top];
    }

    // Check if stack is empty
    public bool IsEmpty()
    {
        return top == -1;
    }
}
```

---

**Time Complexity:**
