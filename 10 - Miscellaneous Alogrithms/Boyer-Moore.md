# Boyer-Moore Algorithm (String Pattern Matching) Implementation in C#

## Algorithm Steps

- Preprocess the pattern to create the bad character heuristic table:
  - For each character in the pattern, store its last occurrence index.
- Start aligning the pattern at the beginning of the text.
- Compare the pattern from right to left with the current window in the text:
  - If a mismatch occurs, use the bad character table to shift the pattern so that the mismatched character in the text aligns with its last occurrence in the pattern (or shift past it if not present).
  - If a match is found, record the index and shift the pattern to align the next possible match.
- Repeat until the pattern has been aligned with all possible windows in the text.

---

## C# Code Example

```csharp
using System;
using System.Collections.Generic;

public class BoyerMoore
{
    private static int NO_OF_CHARS = 256;

    // Preprocess the pattern to create the bad character heuristic table
    private static void BadCharHeuristic(string pattern, int[] badChar)
    {
        for (int i = 0; i < NO_OF_CHARS; i++)
            badChar[i] = -1;
        for (int i = 0; i < pattern.Length; i++)
            badChar[(int)pattern[i]] = i;
    }

    public static void Search(string text, string pattern)
    {
        int m = pattern.Length;
        int n = text.Length;
        int[] badChar = new int[NO_OF_CHARS];

        BadCharHeuristic(pattern, badChar);

        int s = 0; // s is shift of the pattern with respect to text
        while (s <= (n - m))
        {
            int j = m - 1;

            // Keep reducing index j of pattern while characters match
            while (j >= 0 && pattern[j] == text[s + j])
                j--;

            if (j < 0)
            {
                Console.WriteLine("Pattern found at index " + s);

                // Shift pattern so that the next character in text aligns with the last occurrence in pattern
                s += (s + m < n) ? m - badChar[text[s + m]] : 1;
            }
            else
            {
                s += Math.Max(1, j - badChar[text[s + j]]);
            }
        }
    }
}
```

---

## Time and Space Complexity

**Time Complexity**

- Best case: O(n/m), where n is the length of the text and m is the length of the pattern.
- Worst case: O(n \* m), but in practice, it is very efficient for most inputs.

**Space Complexity**

- O(m), for the bad character table.

## Uses

Boyer-Moore algorithm is used for:

- **Efficient substring search** in large texts.
- **Text editors and search tools** for fast pattern matching.
- **Bioinformatics** for
