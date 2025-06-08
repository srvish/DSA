# Trie (Prefix Tree)

A Trie (or Prefix Tree) is a tree data structure used for efficient retrieval of a key in a large dataset of strings. It is commonly used for autocomplete, spell checking, and prefix-based search.

---

## Algorithm Steps

**Insert:**

- Start from the root node.
- For each character in the word:
  - If the character node does not exist, create a new node.
  - Move to the child node corresponding to the character.
- After inserting all characters, mark the last node as the end of a word.

**Search:**

- Start from the root node.
- For each character in the word:
  - If the character node does not exist, return false.
  - Move to the child node corresponding to the character.
- After all characters, check if the last node is marked as the end of a word.

**StartsWith (Prefix Search):**

- Start from the root node.
- For each character in the prefix:
  - If the character node does not exist, return false.
  - Move to the child node corresponding to the character.
- If all characters are found, return true.

---

## C# Implementation

```csharp
public class TrieNode
{
    public TrieNode[] children = new TrieNode[26];
    public bool isWord = false;
}

public class Trie
{
    private TrieNode root;

    public Trie()
    {
        root = new TrieNode();
    }

    // Insert a word into the trie
    public void Insert(string word)
    {
        TrieNode node = root;
        foreach (char c in word)
        {
            int idx = c - 'a';
            if (node.children[idx] == null)
                node.children[idx] = new TrieNode();
            node = node.children[idx];
        }
        node.isWord = true;
    }

    // Search for a word in the trie
    public bool Search(string word)
    {
        TrieNode node = root;
        foreach (char c in word)
        {
            int idx = c - 'a';
            if (node.children[idx] == null)
                return false;
            node = node.children[idx];
        }
        return node.isWord;
    }

    // Check if any word in the trie starts with the given prefix
    public bool StartsWith(string prefix)
    {
        TrieNode node = root;
        foreach (char c in prefix)
        {
            int idx = c - 'a';
            if (node.children[idx] == null)
                return false;
            node = node.children[idx];
        }
        return true;
    }
}
```

---

**Time Complexity:**

- Insert: O(L)
- Search: O(L)
- StartsWith: O(L)  
  Where L is the length of the word or prefix.

**Space Complexity:** O(N \* L)  
Where N is the number of words inserted and L is the average length of the words.
