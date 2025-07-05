# Quick Sort

- Quick Sort is a sorting algorithm based on the divide and conquer approach.
- An array is divided into subarrays by selecting a pivot element.
- The pivot is positioned so that elements less than the pivot are on the left, and elements greater than the pivot are on the right.
- The left and right subarrays are recursively sorted using the same approach.
- This process continues until each subarray contains a single element.
- Finally, the sorted subarrays are combined to form the sorted array.

**Algorithm Steps:**

- Choose a pivot element from the array.
- Partition the array so that elements less than the pivot are on the left, and elements greater than the pivot are on the right.
- Recursively apply the above steps to the left and right subarrays.
- Combine the sorted subarrays.

**Example:**

```csharp
public static void QuickSort(int[] arr)
{
    QuickSort(arr, 0, arr.Length - 1);
}

public static void QuickSort(int[] arr, int low, int high)
{
    if (low < high)
    {
        int pi = Partition(arr, low, high);
        QuickSort(arr, low, pi - 1);
        QuickSort(arr, pi + 1, high);
    }
}

public static int Partition(int[] arr, int low, int high)
{
    int pivot = arr[high];
    int i = low;
    for (int j = low; j < high; j++)
    {
        if (arr[j] < pivot)
        {
            (arr[i], arr[j]) = (arr[j], arr[i]);
            i++;
        }
    }
    (arr[i], arr[high]) = (arr[high], arr[i]);
    return i;
}
```

**Time Complexity:** O(N log N) on average, O(N²) worst case  
**Space Complexity:** O(log N) auxiliary (due to recursion stack)
