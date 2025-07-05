# Merge Sort

- Merge Sort is a popular sorting algorithm based on the Divide and Conquer principle.
- It divides the array into two halves, recursively sorts each half, and then merges the sorted halves.

**Algorithm Steps:**

- Divide the array into two halves.
- Recursively sort each half.
- Merge the two sorted halves into a single sorted array.
- Repeat until the entire array is sorted.

**Example:**

```csharp
public static void MergeSort(int[] arr) {
    MergeSort(arr, 0, arr.Length - 1);
}

static void MergeSort(int[] arr, int l, int r)
{
    if (l == r)
        return;

    int m = (l + r) / 2;
    MergeSort(arr, l, m);
    MergeSort(arr, m + 1, r);
    Merge(arr, l, m, r);
}

static void Merge(int[] arr, int l, int m, int r)
{
    int i = l;
    int j = m + 1;
    Queue<int> q = new Queue<int>();
    while (i <= m && j <= r)
    {
        if (arr[i] <= arr[j])
            q.Enqueue(arr[i++]);
        else
            q.Enqueue(arr[j++]);
    }

    while (i <= m)
        q.Enqueue(arr[i++]);

    while (j <= r)
        q.Enqueue(arr[j++]);

    while (q.Count > 0)
        arr[l++] = q.Dequeue();
}
```

**Time Complexity:** O(N log N)  
**Space Complexity:** O(N)
