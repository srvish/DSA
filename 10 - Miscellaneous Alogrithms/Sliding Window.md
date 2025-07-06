# Sliding Window Technique

## What is Sliding Window?

The **Sliding Window** technique is an efficient way to solve problems that involve linear data structures (like arrays or strings) and require finding subarrays/substrings that satisfy certain conditions (e.g., maximum/minimum sum, length, or unique elements). Instead of checking all possible subarrays, the window "slides" over the data, maintaining a running result and updating it as the window moves.

**Applications:**

- Maximum/minimum sum subarray of size k
- Longest substring with k distinct characters
- Smallest window containing all characters of another string

---

## Algorithm Steps (Fixed-size Window)

- Initialize two pointers (start and end) to represent the window.
- Move the end pointer to expand the window and include new elements.
- When the window reaches the required size, process the result (e.g., update max/min).
- Move the start pointer to shrink the window and continue.

---

## C# Code Example (Maximum Sum Subarray of Size k)

```csharp
using System;

public class SlidingWindow
{
    // Returns the maximum sum of a subarray of size k
    public static int MaxSumSubarray(int[] arr, int k)
    {
        int n = arr.Length;
        if (n < k) return -1;

        int maxSum = 0, windowSum = 0;
        for (int i = 0; i < k; i++)
            windowSum += arr[i];

        maxSum = windowSum;

        for (int i = k; i < n; i++)
        {
            windowSum += arr[i] - arr[i - k];
            maxSum = Math.Max(maxSum, windowSum);
        }
        return maxSum;
    }
}
```

---

## Time and Space Complexity

**Time Complexity**

- O(N), where N is the length of the array.

**Space Complexity**

- O(1), constant extra space.

---

## Uses

- Efficiently solve subarray/substring problems
- Find maximum/minimum sum or length
- Count or track unique elements
