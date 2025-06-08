# Insertion Sort

- Insertion Sort works by selecting a key starting from index 1 and inserting it into its correct position in the sorted part of the array.
- The key is compared with previous elements and swapped until it is greater than the previous element or the beginning of the array is reached.

**Algorithm Steps:**

- Start from the second element (index 1).
- Select the key and compare it with elements to its left.
- Shift elements that are greater than the key to one position ahead.
- Insert the key at the correct position.
- Repeat for all elements until the array is sorted.

**Example:**

```csharp
private static void InsertionSort(int[] arr)
{
    for (int i = 1; i < arr.Length; i++)
    {
        int j = i;
        while (j > 0 && arr[j - 1] > arr[j])
        {
            (arr[j], arr[j - 1]) = (arr[j - 1], arr[j]);
            j--;
        }
    }
}
```

**Time Complexity:** O(N²)  
**Space Complexity:** O(1)
