# Heap Sort

- Heap Sort is a comparison-based sorting algorithm that uses a binary heap data structure.
- It first builds a max heap from the input data.
- The largest element is moved to the end of the array.
- The heap size is reduced and the heap property is restored.
- This process is repeated until the array is sorted.

**Algorithm Steps:**

- Build a max heap from the input array.
- Swap the root (maximum value) with the last element.
- Reduce the heap size by one and heapify the root.
- Repeat the process until the heap size is 1.

**Example:**

```csharp
public static void HeapSort(int[] arr)
{
    for (int i = (arr.Length / 2) - 1; i >= 0; i--)
        Heapify(arr, arr.Length, i);

    for (int i = arr.Length - 1; i >= 0; i--)
    {
        (arr[i], arr[0]) = (arr[0], arr[i]);
        Heapify(arr, i, 0);
    }
}

public static void Heapify(int[] arr, int len, int i)
{
    int max = i;
    int l = i * 2 + 1;
    int r = i * 2 + 2;

    if (l < len && arr[l] > arr[max])
        max = l;

    if (r < len && arr[r] > arr[max])
        max = r;

    if (max != i)
    {
        (arr[max], arr[i]) = (arr[i], arr[max]);
        Heapify(arr, len, max);
    }
}
```

**Time Complexity:** O(N log N)  
**Space Complexity:** O(1)
