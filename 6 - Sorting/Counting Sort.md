# Counting Sort

- Counting Sort is a non-comparison-based sorting algorithm that works efficiently for sorting integers within a known, limited range.
- It only works with non-negative integers.

**Algorithm Steps:**

- Find the maximum value in the array.
- Create a count array to store the frequency of each value.
- Update the count array to store cumulative counts.
- Build the output array by placing elements at their correct positions using the count array.
- Copy the sorted elements back to the original array.

**Example:**

```csharp
public static void CountingSort(int[] arr)
{
    int max = 0;
    // Find the maximum value
    for (int i = 0; i < arr.Length; i++)
        if (max < arr[i])
            max = arr[i];

    int[] na = new int[max + 1];
    // Count the occurrences
    for (int i = 0; i < arr.Length; i++)
        na[arr[i]]++;

    // Cumulative count
    for (int i = 1; i < na.Length; i++)
        na[i] += na[i - 1];

    int[] op = new int[arr.Length];
    // Build the output array
    for (int i = arr.Length - 1; i >= 0; i--)
        op[--na[arr[i]]] = arr[i];

    // Copy back to original array
    for (int i = 0; i < op.Length; i++)
        arr[i] = op[i];
}
```

**Time Complexity:** O(N + K)  
**Space Complexity:** O(N + K)  
Where N is the number of elements and K is the range of input.
