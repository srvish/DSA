# Huffman Coding

## What is Huffman Coding?

**Huffman Coding** is a greedy algorithm used for lossless data compression. It assigns variable-length codes to input characters, with shorter codes assigned to more frequent characters. The result is a prefix code (no code is a prefix of another), which ensures efficient and unambiguous decoding.

**Applications:**

- File compression (ZIP, GZIP)
- Image compression (JPEG)
- Data transmission

---

## Algorithm Steps

- Count the frequency of each character in the input.
- Create a priority queue (min-heap) of nodes, each containing a character and its frequency.
- While there is more than one node in the queue:
  - Remove the two nodes with the lowest frequency.
  - Create a new internal node with these two nodes as children and frequency equal to the sum of their frequencies.
  - Insert the new node back into the queue.
- The remaining node is the root of the Huffman tree.
- Assign codes to characters by traversing the tree (left = 0, right = 1).

---

## C# Code Example

```csharp
using System;
using System.Collections.Generic;

public class HuffmanNode : IComparable<HuffmanNode>
{
    public char Char;
    public int Freq;
    public HuffmanNode Left, Right;

    public HuffmanNode(char c, int f)
    {
        Char = c;
        Freq = f;
        Left = Right = null;
    }

    public int CompareTo(HuffmanNode other)
    {
        return this.Freq - other.Freq;
    }
}

public class HuffmanCoding
{
    public static void BuildHuffmanTree(Dictionary<char, int> freq)
    {
        var pq = new SortedSet<HuffmanNode>(Comparer<HuffmanNode>.Create((a, b) =>
            a.Freq == b.Freq ? a.Char.CompareTo(b.Char) : a.Freq - b.Freq));

        foreach (var kv in freq)
            pq.Add(new HuffmanNode(kv.Key, kv.Value));

        while (pq.Count > 1)
        {
            var left = pq.Min; pq.Remove(left);
            var right = pq.Min; pq.Remove(right);

            var sum = new HuffmanNode('\0', left.Freq + right.Freq)
            {
                Left = left,
                Right = right
            };
            pq.Add(sum);
        }

        var root = pq.Min;
        PrintCodes(root, "");
    }

    private static void PrintCodes(HuffmanNode root, string str)
    {
        if (root == null)
            return;

        if (root.Char != '\0')
            Console.WriteLine(root.Char + ": " + str);

        PrintCodes(root.Left, str + "0");
        PrintCodes(root.Right, str + "1");
    }
}
```

---

## Time and Space Complexity

**Time Complexity**

- O(n log n), where n is the number of unique characters (due to priority queue operations).

**Space Complexity**

- O(n), for the tree and frequency table.

---

## Uses

- Efficient data
