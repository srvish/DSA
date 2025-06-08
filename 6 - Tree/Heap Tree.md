# Heap Tree (Min Heap & Max Heap)

A Heap is a complete binary tree that satisfies the heap property:

- **Max Heap:** Parent is greater than or equal to its children.
- **Min Heap:** Parent is less than or equal to its children.

---

## Algorithm Steps

**Insert:**

- Add the new element at the end of the heap (array).
- "Heapify up": Compare with its parent and swap if the heap property is violated.
- Repeat until the heap property is restored.

**Extract (Remove Root):**

- Remove the root element (min or max).
- Move the last element to the root.
- "Heapify down": Compare with children and swap with the appropriate child if the heap property is violated.
- Repeat until the heap property is restored.

---

## C# Implementation

### Max Heap

```csharp
public class MaxHeap
{
    private List<int> heap = new List<int>();

    public void Insert(int val)
    {
        heap.Add(val);
        int i = heap.Count - 1;
        while (i > 0 && heap[(i - 1) / 2] < heap[i])
        {
            (heap[(i - 1) / 2], heap[i]) = (heap[i], heap[(i - 1) / 2]);
            i = (i - 1) / 2;
        }
    }

    public int ExtractMax()
    {
        if (heap.Count == 0) throw new InvalidOperationException("Heap is empty");
        int max = heap[0];
        heap[0] = heap[heap.Count - 1];
        heap.RemoveAt(heap.Count - 1);
        HeapifyDown(0);
        return max;
    }

    private void HeapifyDown(int i)
    {
        int left = 2 * i + 1, right = 2 * i + 2, largest = i;
        if (left < heap.Count && heap[left] > heap[largest]) largest = left;
        if (right < heap.Count && heap[right] > heap[largest]) largest = right;
        if (largest != i)
        {
            (heap[i], heap[largest]) = (heap[largest], heap[i]);
            HeapifyDown(largest);
        }
    }
}
```

### Min Heap

```csharp
public class MinHeap
{
    private List<int> heap = new List<int>();

    public void Insert(int val)
    {
        heap.Add(val);
        int i = heap.Count - 1;
        while (i > 0 && heap[(i - 1) / 2] > heap[i])
        {
            (heap[(i - 1) / 2], heap[i]) = (heap[i], heap[(i - 1) / 2]);
            i = (i - 1) / 2;
        }
    }

    public int ExtractMin()
    {
        if (heap.Count == 0) throw new InvalidOperationException("Heap is empty");
        int min = heap[0];
        heap[0] = heap[heap.Count - 1];
        heap.RemoveAt(heap.Count - 1);
        HeapifyDown(0);
        return min;
    }

    private void HeapifyDown(int i)
    {
        int left = 2 * i + 1, right = 2 * i + 2, smallest = i;
        if (left < heap.Count && heap[left] < heap[smallest]) smallest = left;
        if (right < heap.Count && heap[right] < heap[smallest]) smallest = right;
        if (smallest != i)
        {
            (heap[i], heap[smallest]) = (heap[smallest], heap[i]);
            HeapifyDown(smallest);
        }
    }
}
```

---

**Time Complexity:**

- Insert: O(log N)
- Extract (Remove Root): O(log N)
- Build Heap: O(N)

**Space Complexity:** O(N)
