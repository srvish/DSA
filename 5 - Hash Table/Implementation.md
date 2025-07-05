# HashTable Implementation in C#

## Algorithm Steps

- Initialize an array of buckets (each bucket can be a list for handling collisions).
- **Hash Function:**
  - Compute an index from the key using a hash function.
- **Insert (Add key-value pair):**
  - Compute the hash index for the key.
  - If the bucket at that index is empty, create a new list.
  - Add the key-value pair to the bucket (update if key exists).
- **Search (Get value by key):**
  - Compute the hash index for the key.
  - Search the bucket for the key and return its value if found.
- **Delete (Remove key-value pair):**
  - Compute the hash index for the key.
  - Search the bucket and remove the key-value pair if it exists.

---

## C# Code Example

```csharp
// Simple HashTable implementation using separate chaining
public class HashTable
{
    private class Entry
    {
        public string Key;
        public int Value;
        public Entry(string key, int value)
        {
            Key = key;
            Value = value;
        }
    }

    private List<Entry>[] buckets;
    private int size;

    public HashTable(int capacity)
    {
        size = capacity;
        buckets = new List<Entry>[size];
    }

    private int GetBucketIndex(string key)
    {
        return Math.Abs(key.GetHashCode()) % size;
    }

    // Insert or update key-value pair
    public void Insert(string key, int value)
    {
        int index = GetBucketIndex(key);
        if (buckets[index] == null)
            buckets[index] = new List<Entry>();

        foreach (var entry in buckets[index])
        {
            if (entry.Key == key)
            {
                entry.Value = value;
                return;
            }
        }
        buckets[index].Add(new Entry(key, value));
    }

    // Search for a value by key
    public int? Search(string key)
    {
        int index = GetBucketIndex(key);
        if (buckets[index] != null)
        {
            foreach (var entry in buckets[index])
            {
                if (entry.Key == key)
                    return entry.Value;
            }
        }
        return null;
    }

    // Delete a key-value pair
    public void Delete(string key)
    {
        int index = GetBucketIndex(key);
        if (buckets[index] != null)
        {
            buckets[index].RemoveAll(e => e.Key == key);
        }
    }
}
```

## Time and Space Complexity

**Time Complexity**

- **Insert:** O(1) average, O(n) worst case (if many collisions)
- **Search:** O(1) average, O(n) worst case
- **Delete:** O(1) average, O(n) worst case

**Space Complexity:** O(n + m), where n is the number of elements and m is the number of buckets.
