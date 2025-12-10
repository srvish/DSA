# Manacher's Algorithm

## Problem Statement

Find the longest palindromic substring in a given string in linear time.

## Algorithm Steps

- Transform the input string by inserting a special character (e.g., `#`) between each character and at the boundaries to handle even-length palindromes.
- Initialize an array to store the radius of the palindrome at each position.
- Use two pointers, `center` and `right`, to keep track of the center and right boundary of the current palindrome.
- For each position:
  - Mirror the current position with respect to the center.
  - If within the right boundary, set the initial palindrome radius.
  - Expand the palindrome centered at the current position.
  - Update the center and right boundary if the palindrome expands beyond the current right boundary.
- Find the maximum value in the radius array to get the longest palindromic substring.

## C# Implementation

```csharp
public string LongestPalindromicSubstring(string s)
{
	if (string.IsNullOrEmpty(s)) return "";

	// Transform the string
	var t = new StringBuilder("^");
	foreach (char c in s)
	{
		t.Append("#");
		t.Append(c);
	}
	t.Append("#$");
	string str = t.ToString();

	int n = str.Length;
	int[] p = new int[n];
	int center = 0, right = 0;

	for (int i = 1; i < n - 1; i++)
	{
		int mirror = 2 * center - i;
		if (i < right)
			p[i] = Math.Min(right - i, p[mirror]);

		// Expand around center i
		while (str[i + (1 + p[i])] == str[i - (1 + p[i])])
			p[i]++;

		// Update center and right boundary
		if (i + p[i] > right)
		{
			center = i;
			right = i + p[i];
		}
	}

	// Find the maximum palindrome length
	int maxLen = 0, centerIndex = 0;
	for (int i = 1; i < n - 1; i++)
	{
		if (p[i] > maxLen)
		{
			maxLen = p[i];
			centerIndex = i;
		}
	}

	int start = (centerIndex - maxLen) / 2;
	return s.Substring(start, maxLen);
}
```

## Time Complexity

- O(N), where N is the length of the input string.

## Space Complexity

- O(N), for the transformed string and the palindrome radius array.
