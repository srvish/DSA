# Array Implementation in C#

## Algorithm Steps

- Initialize an array with a fixed size.
- **Insert an element:**
  - Assign the value to the desired index.
- **Access an element:**
  - Retrieve the value at a specific index.
- **Update an element:**
  - Assign a new value to a specific index.
- **Delete an element:**
  - Set the value at a specific index to a default value (e.g., 0 or null).

---

## C# Code Example

```csharp
// Simple Array operations in C#
public class ArrayExample
{
    private int[] arr;

    public ArrayExample(int size)
    {
        arr = new int[size];
    }

    // Insert value at index
    public void Insert(int index, int value)
    {
        if (index < 0 || index >= arr.Length)
            throw new IndexOutOfRangeException("Index out of bounds");
        arr[index] = value;
    }

    // Access value at index
    public int Access(int index)
    {
        if (index < 0 || index >= arr.Length)
            throw new IndexOutOfRangeException("Index out of bounds");
        return arr[index];
    }

    // Update value at index
    public void Update(int index, int value)
    {
        if (index < 0 || index >= arr.Length)
            throw new IndexOutOfRangeException("Index out of bounds");
        arr[index] = value;
    }

    // Delete value at index (set to 0)
    public void Delete(int index)
    {
        if (index < 0 || index >= arr.Length)
            throw new IndexOutOfRangeException("Index out of bounds");
        arr[index] = 0;
    }
}
```

## Time and Space Complexity

**Time Complexity**

- **Insert:** O(1)
- **Access:** O(1)
- **Update:** O(1)
- **Delete:** O(1)

**Space Complexity:** O(n), where n is the size of the array.
