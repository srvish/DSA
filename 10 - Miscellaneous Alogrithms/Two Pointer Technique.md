# Two Pointer Technique

## What is Two Pointer Technique?

The **Two Pointer Technique** is a common algorithmic approach used to solve problems involving linear data structures (like arrays or strings). It uses two pointers (indices) that move through the data structure, often from opposite ends or at different speeds, to efficiently solve problems such as searching pairs, reversing, or partitioning.

**Applications:**

- Finding pairs with a given sum in a sorted array
- Reversing arrays or strings
- Removing duplicates
- Partitioning arrays
- Merging sorted arrays

---

## Algorithm Steps (Example: Find if a pair with a given sum exists in a sorted array)

- Initialize two pointers: `left` at the start and `right` at the end of the array.
- While `left < right`:
  - Calculate the sum of elements at `left` and `right`.
  - If the sum equals the target, return true (pair found).
  - If the sum is less than the target, increment `left` to increase the sum.
  - If the sum is greater than the target, decrement `right` to decrease the sum.
- If no such pair is found, return false.

---

## C# Code Example (Pair Sum in Sorted Array)

```csharp
using System;

public class TwoPointer
{
    // Returns true if there is a pair with the given sum
    public static bool HasPairWithSum(int[] arr, int target)
    {
        int left = 0, right = arr.Length - 1;
        while (left < right)
        {
            int sum = arr[left] + arr[right];
            if (sum == target)
                return true;
            else if (sum < target)
                left++;
            else
                right--;
        }
        return false;
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

- Efficient searching and partitioning in arrays
- Solving subarray/subsequence problems
- Removing duplicates or specific elements
- Merging sorted arrays or lists
