# Bubble Sort

- Bubble Sort works by comparing each element with the next element.
- If the current element is larger, swap it with the next.
- Repeat this process for all elements in the array.
- After each pass, the largest unsorted element moves to its correct position at the end of the array.
- This process is repeated until the entire array is sorted.

**Example:**

```csharp
public static void BubbleSort(int[] arr)
{
    for (int i = 0; i < arr.Length - 1; i++)
    {
        for (int j = 0; j < arr.Length - i - 1; j++)
        {
            if (arr[j] > arr[j + 1])
                (arr[j], arr[j + 1]) = (arr[j + 1], arr[j]);
        }
    }
}
```

**Time Complexity:** O(N²)  
**Space Complexity:** O(1)
