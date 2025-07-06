# Knuth-Morris-Pratt (KMP) Algorithm (String Pattern Matching) Implementation in C#

## Algorithm Steps

- Preprocess the pattern to create the Longest Prefix Suffix (LPS) array:
  - For each position in the pattern, store the length of the longest prefix which is also a suffix.
- Use the LPS array to avoid unnecessary comparisons while searching:
  - Compare the pattern with the text from left to right.
  - If a mismatch occurs after some matches, use the LPS array to skip characters in the pattern, not the text.
- Repeat until the end of the text.

---

## C# Code Example

```csharp
using System;

public class KMP
{
    // Preprocess the pattern to create LPS array
    private static void ComputeLPSArray(string pattern, int m, int[] lps)
    {
        int len = 0;
        lps[0] = 0;
        int i = 1;
        while (i < m)
        {
            if (pattern[i] == pattern[len])
            {
                len++;
                lps[i] = len;
                i++;
            }
            else
            {
                if (len != 0)
                {
                    len = lps[len - 1];
                }
                else
                {
                    lps[i] = 0;
                    i++;
                }
            }
        }
    }

    public static void KMPSearch(string pattern, string text)
    {
        int m = pattern.Length;
        int n = text.Length;
        int[] lps = new int[m];

        ComputeLPSArray(pattern, m, lps);

        int i = 0; // index for text
        int j = 0; // index for pattern
        while (i < n)
        {
            if (pattern[j] == text[i])
            {
                i++;
                j++;
            }
            if (j == m)
            {
                Console.WriteLine("Pattern found at index " + (i - j));
                j = lps[j - 1];
            }
            else if (i < n && pattern[j] != text[i])
            {
                if (j != 0)
                    j = lps[j - 1];
                else
                    i++;
            }
        }
    }
}
```

---

## Time and Space Complexity

**Time Complexity**

- O(n + m), where n is the length of the text and m is the length of the pattern.

**Space Complexity**

- O(m), for the LPS array.

## Uses

KMP algorithm is used for:

- **Efficient substring search** in large texts.
- **Pattern matching** in editors, search engines, and bioinformatics.
- **Detecting repeated patterns** in strings.
