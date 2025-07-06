# Rabin-Karp Algorithm (String Pattern Matching) Implementation in C#

## Algorithm Steps

- Choose a hash function and a prime number for modulo operations.
- Compute the hash value of the pattern and the first window of the text.
- Slide the pattern over the text one by one:
  - For each window, compare the hash value of the current text window with the pattern's hash value.
  - If the hash values match, check the characters one by one to confirm a match.
  - Compute the hash value for the next window using a rolling hash formula.
- Repeat until the end of the text.

---

## C# Code Example

```csharp
using System;

public class RabinKarp
{
    public static void Search(string text, string pattern)
    {
        int d = 256; // Number of characters in the input alphabet
        int q = 101; // A prime number
        int m = pattern.Length;
        int n = text.Length;
        int p = 0; // Hash value for pattern
        int t = 0; // Hash value for text
        int h = 1;

        // The value of h would be "pow(d, m-1)%q"
        for (int i = 0; i < m - 1; i++)
            h = (h * d) % q;

        // Calculate the hash value of pattern and first window of text
        for (int i = 0; i < m; i++)
        {
            p = (d * p + pattern[i]) % q;
            t = (d * t + text[i]) % q;
        }

        // Slide the pattern over text one by one
        for (int i = 0; i <= n - m; i++)
        {
            // Check the hash values of current window of text and pattern
            if (p == t)
            {
                // If the hash values match, check characters one by one
                int j;
                for (j = 0; j < m; j++)
                {
                    if (text[i + j] != pattern[j])
                        break;
                }
                if (j == m)
                    Console.WriteLine("Pattern found at index " + i);
            }

            // Calculate hash value for next window of text
            if (i < n - m)
            {
                t = (d * (t - text[i] * h) + text[i + m]) % q;
                if (t < 0)
                    t = (t + q);
            }
        }
    }
}
```

---

## Time and Space Complexity

**Time Complexity**

- Average and best case: O(n + m), where n is the length of the text and m is the length of the pattern.
- Worst case: O(nm), when many hash collisions occur.

**Space Complexity**

- O(1), auxiliary space.

## Uses

Rabin-Karp algorithm is used for:

- **Efficient substring search** in large texts.
- **Plagiarism detection** (finding common substrings).
- **Detecting multiple patterns** in a text (with minor modifications).
