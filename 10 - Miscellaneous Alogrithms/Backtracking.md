# Backtracking

## What is Backtracking?

**Backtracking** is a general algorithmic technique for solving problems recursively by trying to build a solution incrementally, one piece at a time, and removing those solutions that fail to satisfy the constraints of the problem at any point (i.e., backtrack and try another possibility).

**Applications:**

- Solving puzzles (Sudoku, N-Queens, Crossword)
- Combinatorial problems (permutations, combinations, subsets)
- Pathfinding (maze, rat in a maze)
- Constraint satisfaction problems

---

## Algorithm Steps

- Start from an initial state and try to extend the solution step by step.
- At each step:
  - Check if the current solution is valid (satisfies constraints).
  - If valid and complete, record or print the solution.
  - If not complete, recursively try all possible extensions.
  - If an extension leads to a dead end, backtrack (remove the last step and try another).

---

## C# Code Example (N-Queens Problem)

```csharp
using System;
using System.Collections.Generic;

public class NQueens
{
    public static void SolveNQueens(int n)
    {
        int[] board = new int[n];
        List<List<string>> solutions = new List<List<string>>();
        PlaceQueen(board, 0, n, solutions);
        PrintSolutions(solutions);
    }

    private static void PlaceQueen(int[] board, int row, int n, List<List<string>> solutions)
    {
        if (row == n)
        {
            solutions.Add(BuildBoard(board, n));
            return;
        }
        for (int col = 0; col < n; col++)
        {
            if (IsSafe(board, row, col))
            {
                board[row] = col;
                PlaceQueen(board, row + 1, n, solutions);
            }
        }
    }

    private static bool IsSafe(int[] board, int row, int col)
    {
        for (int i = 0; i < row; i++)
        {
            if (board[i] == col || Math.Abs(board[i] - col) == row - i)
                return false;
        }
        return true;
    }

    private static List<string> BuildBoard(int[] board, int n)
    {
        var res = new List<string>();
        for (int i = 0; i < n; i++)
        {
            char[] row = new char[n];
            Array.Fill(row, '.');
            row[board[i]] = 'Q';
            res.Add(new string(row));
        }
        return res;
    }

    private static void PrintSolutions(List<List<string>> solutions)
    {
        foreach (var solution in solutions)
        {
            foreach (var row in solution)
                Console.WriteLine(row);
            Console.WriteLine();
        }
    }
}
```

---

## Time and Space Complexity

**Time Complexity**

- Exponential in the worst case (e.g., O(N!) for N-Queens).

**Space Complexity**

- O(N), for the recursion stack and board representation.

---

## Uses

- Solving constraint satisfaction and combinatorial problems
- Generating all possible configurations or solutions
- Finding paths or arrangements under constraints
