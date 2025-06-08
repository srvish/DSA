# Suffix Tree & Suffix Array

A **Suffix Tree** is a compressed trie of all the suffixes of a given string.  
A **Suffix Array** is a sorted array of all suffixes of a string.

Suffix Arrays are easier to implement and are widely used for pattern matching, substring search, and other string processing problems.

---

## Suffix Array

**Algorithm Steps:**

- Generate all suffixes of the string along with their starting indices.
- Sort the suffixes lexicographically.
- Store the starting indices of the sorted suffixes in an array.

---

### C# Implementation (Suffix Array)

```csharp
public class SuffixArray
{
    public int[] BuildSuffixArray(string s)
    {
        int n = s.Length;
        var suffixes = new List<(string suffix, int index)>();
        for (int i = 0; i < n; i++)
            suffixes.Add((s.Substring(i), i));
        suffixes.Sort((a, b) => string.Compare(a.suffix, b.suffix, StringComparison.Ordinal));
        int[] sa = new int[n];
        for (int i = 0; i < n; i++)
            sa[i] = suffixes[i].index;
        return sa;
    }
}
```

---

## Suffix Tree (Conceptual, simplified)

Suffix Trees are complex to implement efficiently. Below is a very basic and non-optimized version for educational purposes.

**Algorithm Steps:**

- For each suffix of the string, insert it into a trie structure.
- Each edge represents a substring of the original string.

---

### C# Implementation (Suffix Tree - Simplified)

```csharp
public class SuffixTreeNode
{
    public Dictionary<char, SuffixTreeNode> Children = new Dictionary<char, SuffixTreeNode>();
}

public class SuffixTree
{
    private SuffixTreeNode root = new SuffixTreeNode();

    public void Build(string s)
    {
        for (int i = 0; i < s.Length; i++)
        {
            SuffixTreeNode node = root;
            for (int j = i; j < s.Length; j++)
            {
                char c = s[j];
                if (!node.Children.ContainsKey(c))
                    node.Children[c] = new SuffixTreeNode();
                node = node.Children[c];
            }
        }
    }
}
```

---

**Time Complexity:**

- Suffix Array: O(N² log N) (naive), O(N log N) (optimized algorithms)
- Suffix Tree: O(N²) (naive), O(N) (Ukkonen's algorithm, not shown here)

**Space Complexity:**

- Suffix Array: O(N)
- Suffix Tree: O(N²) (naive), O(N) (optimized)
