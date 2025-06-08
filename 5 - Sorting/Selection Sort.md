# Selection Sort

- Selection Sort works by selecting the minimum element in the unsorted part of the array and swapping it with the first unsorted element.
- Repeat this process for each position in the array until the entire array is sorted.

**Algorithm Steps:**

- Start from the first element and assume it is the minimum.
- Compare this element with the rest of the array to find the actual minimum.
- Swap the found minimum element with the first element.
- Move to the next position and repeat the process for the remaining unsorted part of the array.
- Continue until the array is completely sorted.

**Example:**

```csharp
public static void SelectionSort(int[] arr)
{
    for (int i = 0; i < arr.Length - 1; i++)
    {
        int minIndex = i;
        for (int j = i + 1; j < arr.Length; j++)
        {
            if (arr[minIndex] > arr[j])
                minIndex = j;
        }
        (arr[minIndex], arr[i]) = (arr[i], arr[minIndex]);
    }
}
```

**Time Complexity:** O(N²)  
**Space Complexity:** O(1)
