# Knapsack Problem and Algorithm

## What is Knapsack?

The **Knapsack problem** is a classic optimization problem. Given a set of items, each with a weight and a value, and a knapsack with a weight capacity, the goal is to select a subset of items to maximize the total value without exceeding the knapsack's weight limit.

- **0/1 Knapsack:** Each item can be included at most once (cannot be broken).
- **Fractional Knapsack:** Items can be broken into smaller parts (fractions can be taken).

---

## Algorithm Steps (0/1 Knapsack, Dynamic Programming)

- Create a DP table `dp[n+1][W+1]` where `n` is the number of items and `W` is the knapsack capacity.
- For each item `i` (1 to n) and each capacity `w` (0 to W):
  - If the item's weight is less than or equal to `w`:
    - `dp[i][w] = max(dp[i-1][w], value[i-1] + dp[i-1][w - weight[i-1]])`
  - Else:
    - `dp[i][w] = dp[i-1][w]`
- The answer is `dp[n][W]`.

---

## C# Code Example (0/1 Knapsack, Dynamic Programming)

```csharp
using System;

public class Knapsack
{
    // Returns the maximum value that can be put in a knapsack of capacity W
    public static int Knapsack01(int[] weights, int[] values, int W)
    {
        int n = weights.Length;
        int[,] dp = new int[n + 1, W + 1];

        for (int i = 0; i <= n; i++)
        {
            for (int w = 0; w <= W; w++)
            {
                if (i == 0 || w == 0)
                    dp[i, w] = 0;
                else if (weights[i - 1] <= w)
                    dp[i, w] = Math.Max(dp[i - 1, w], values[i - 1] + dp[i - 1, w - weights[i - 1]]);
                else
                    dp[i, w] = dp[i - 1, w];
            }
        }
        return dp[n, W];
    }
}
```

---

## Time and Space Complexity

**Time Complexity**

- O(N \* W), where N is the number of items and W is the knapsack capacity.

**Space Complexity**

- O(N \* W), for the DP table.

---

## Applications

- Resource allocation
- Budget management
- Cargo
