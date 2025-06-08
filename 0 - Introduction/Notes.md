Mail: mailithere24@gmail.com

## Useful Links

- https://seanprashad.com/leetcode-patterns/
- https://github.com/hxu296/leetcode-company-wise-problems-2022
- https://www.programiz.com/dsa
- https://www.geeksforgeeks.org/c-program-to-print-all-permutations-of-a-given-string-2/

## Interview Tips

- For specific roles, expect technical questions related to the language/framework.
- For MAANG, focus on concepts, not language. Explain logic before coding.
- Update your resume to show quantitative achievements, not just skills.
- Highlight features and performance improvements.

## Index

1. Introduction
2. Linear vs Non-Linear Data Structures
3. Tree
4. Graph
5. Sorting
6. Searching
7. Greedy Algorithms
8. Dynamic Programming
9. Extra Algorithms

## Introduction

**What is a Data Structure?**

- A way to store and organize data for efficient access and updates.

**Types of Data Structures**

- Linear: Stores data sequentially
  - Array
  - Stack
  - Queue
  - Linked List
- Non-Linear: Stores data non-sequentially
  - Tree (Binary Tree, Binary Search Tree, AVL Tree, B-Tree, B+Tree, Red-Black Tree)
  - Graph (Spanning Tree, Minimum Spanning Tree, Strongly Connected Component, Adjacency Matrix/List)

## Asymptotic Analysis

- **Big O**: Upper bound (worst-case)
- **Omega**: Lower bound (best-case)
- **Theta**: Tight bound (average-case)
- **Note**:
  - Focus on Big O for interviews (worst-case).
  - Ignore constants and less dominant terms.
  - Time complexity order: O(1) < O(logN) < O(N) < O(NlogN) < O(N²logN) < O(N³)
  - Space complexity = auxiliary space + input space. Don’t modify input unless asked.

## Master Theorem

- Used for analyzing divide and conquer recurrences.

## Divide and Conquer

- Break a problem into subproblems, solve recursively, and combine results.
- Examples: Binary Search, Merge Sort, Quick Sort, Strassen's Matrix Multiplication, Karatsuba Algorithm

## Linear Data Structures Details

**Stack** (LIFO)

- Operations: Push, Pop, Peek, IsEmpty, IsFull
- Examples: Reverse word, expression evaluation, browser back button

**Queue** (FIFO)

- Operations: Enqueue, Dequeue, IsEmpty, IsFull, Peek
- Types: Circular Queue, Deque, Priority Queue
- Examples: CPU scheduling, Disk scheduling

**Array**

- Stores records sequentially
- Algorithms: Kadane's, Sliding Window, Two Pointers, Prefix Sums

**Linked List**

- Types: Singly, Doubly, Circular
- Algorithms: Fast/slow pointer (find middle, detect loop, delete from back)

**Hash Table**

- Stores key-value pairs using a hash function.
- Collision resolution: Separate chaining (open hashing), Linear probing (closed hashing)

## Tree Data Structures

**Tree Terminology**

- Node, Edge, Root, Height, Depth, Degree, Forest

**Tree Traversal**

- In-order, Pre-order, Post-order, Level-order (recursive and non-recursive)

**Types of Trees**

- Binary Tree (Full, Perfect, Complete, Degenerate, Skewed, Balanced)
- Binary Search Tree (BST): O(logN) search/insert/delete
- AVL Tree: Self-balancing BST
- B-Tree: Multi-key, multi-child, height-balanced, used for disk storage
- B+ Tree: All values at leaf level, supports multilevel indexing
- Red-Black Tree: Self-balancing BST
- Trie (Prefix Tree): Efficient insert/search/startsWith for strings
- Union-Find, Segment Tree, Fenwick Tree (Binary Indexed Tree), Heap, Suffix Tree/Array, Disjoint Set

**Heap**

- Complete binary tree with the heap property (max/min)
- Operations: Heapify, Insert, Remove, Priority Queue
- Used in Heap Sort

## Graph Data Structures

**Terminology**

- Vertex, Edge, Adjacency, Path, Directed/Undirected Graph

**Representation**

- Adjacency Matrix, Adjacency List

**Operations**

- Check presence, traversal, add vertex/edge, find path

**Traversal**

- BFS (uses queue): Level order, shortest path in unweighted graphs
- DFS (uses stack/recursion): Topological sort, cycle detection

**Spanning Tree**

- Subgraph including all vertices with minimum edges
- Minimum Spanning Tree: Prim’s, Kruskal’s algorithms

**Strongly Connected Components**

- Find using Kosaraju’s Algorithm

**Shortest Path Algorithms**

- Dijkstra’s (weighted graphs, no negative weights)
- Bellman-Ford (handles negative weights)
- Prim’s, Topological Sort

## Sorting Algorithms

1. **Bubble Sort**: Compare and swap adjacent elements. O(N²)
2. **Selection Sort**: Select min and swap with start. O(N²)
3. **Insertion Sort**: Insert key in sorted part. O(N²)
4. **Merge Sort**: Divide and merge. O(NlogN)
5. **Quick Sort**: Partition around pivot. O(NlogN) average
6. **Counting Sort**: Count occurrences. O(N+K), only for positive numbers
7. **Heap Sort**: Build heap, extract max/min. O(NlogN)

## Searching Algorithms

1. **Linear Search**
2. **Binary Search**

## Greedy Algorithms

- Approach: Make the best choice at each step; may not be globally optimal.
- Properties: Greedy choice property, optimal substructure
- Examples: Selection Sort, Knapsack, MST, Job Scheduling, Dijkstra, Huffman Coding, Ford-Fulkerson

## Dynamic Programming

- Efficient for overlapping subproblems and optimal substructure.
- Store solutions to subproblems to avoid recomputation.
- Examples: Floyd-Warshall, Longest Common Subsequence, 0/1 Knapsack, Palindromes

## Extra Algorithms

- Backtracking
- Rabin-Karp (Rolling Hash)
- Knuth-Morris-Pratt (KMP)
- Boyer-Moore (Majority Voting)
