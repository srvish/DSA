Mail: mailithere24@gmail.com

## Interview Tips

- For specific roles, expect technical questions related to the language/framework.
- For MAANG, focus on concepts, not language. Explain logic before coding.
- Update your resume to show quantitative achievements, not just skills.
- Highlight features and performance improvements.

## Index

1. Introduction
2. Array
3. Stack
4. Queue
5. Array
6. Linked List
7. Tree
8. Graph
9. Sorting
10. Searching
11. Greedy Algorithms
12. Dynamic Programming
13. Extra Algorithms

# <h1 align=center>Introduction</h1>

**What is a Data Structure?**

- A way to store and organize data for efficient access and updates.

**Asymptotic Analysis**

- **Big O**: Upper bound (worst-case)
- **Omega**: Lower bound (best-case)
- **Theta**: Tight bound (average-case)
- **Note**:
  - Focus on Big O for interviews (worst-case).
  - Ignore constants and less dominant terms.
  - Time complexity order: O(1) < O(logN) < O(N) < O(NlogN) < O(N²logN) < O(N³)
  - Space complexity = auxiliary space + input space. Don’t modify input unless asked.

**Master Theorem**

- Used for analyzing divide and conquer recurrences.

**Divide and Conquer**

- Break a problem into subproblems, solve recursively, and combine results.
- Examples: Binary Search, Merge Sort, Quick Sort, Strassen's Matrix Multiplication, Karatsuba Algorithm

**Types of Data Structures**

- Linear: Stores data sequentially. Example: Array, Stack, Queue, Linked List
- Non-Linear: Stores data non-sequentially
  - Tree (Binary Tree, Binary Search Tree, AVL Tree, B-Tree, B+Tree, Red-Black Tree)
  - Graph (Spanning Tree, Minimum Spanning Tree, Strongly Connected Component, Adjacency Matrix/List)

# <h1 align=center>Stack</h1>

[**Stack**](1%20-%20Stack/Implementation.md) (LIFO)

- Operations: Push, Pop, Peek, IsEmpty, IsFull
- Examples: Reverse word, expression evaluation, browser back button

# <h1 align=center>Queue</h1>

[**Queue**](2%20-%20Queue/Implementation.md) (FIFO)

- Operations: Enqueue, Dequeue, IsEmpty, IsFull, Peek
- Types: Circular Queue, Deque, Priority Queue
- Examples: CPU scheduling, Disk scheduling

# <h1 align=center>Array</h1>

[**Array**](3%20-%20Array/Implementation.md)

- Stores records sequentially
- Algorithms: Kadane's, Sliding Window, Two Pointers, Prefix Sums

# <h1 align=center>Linked List</h1>

[**Linked List**](4%20-%20Linked%20List/Implementation.md)

- Types: Singly, Doubly, Circular
- Algorithms: Fast/slow pointer (find middle, detect loop, delete from back)

# <h1 align=center>Hash Table</h1>

[**Hash Table**](5%20-%20Hash%20Table/Implementation.md)

- Stores key-value pairs using a hash function.
- Collision resolution: Separate chaining (open hashing), Linear probing (closed hashing)

# <h1 align=center>Tree</h1>

**Tree Terminology**

- Node, Edge, Root, Height, Depth, Degree, Forest

**Tree Traversal**

- [In-order](7%20-%20Tree/Inorder%20Traversal.md), [Pre-order](7%20-%20Tree/Preorder%20Traversal.md), [Post-order](7%20-%20Tree/Postorder%20Traversal.md), [Level-order](7%20-%20Tree/Levelorder%20Traversal.md) (recursive and non-recursive)

**Types of Trees**

- Binary Tree (Full, Perfect, Complete, Degenerate, Skewed, Balanced)
- [Binary Search Tree (BST)](7%20-%20Tree/Binary%20Search%20Tree.md): O(logN) search/insert/delete
- [AVL Tree](7%20-%20Tree/AVL%20Tree.md): Self-balancing BST
- [B-Tree](7%20-%20Tree/B-Tree.md): Multi-key, multi-child, height-balanced, used for disk storage
- [B+ Tree](7%20-%20Tree/B+Tree.md): All values at leaf level, supports multilevel indexing
- [Red-Black Tree](7%20-%20Tree/Red%20Block%20Tree.md): Self-balancing BST
- [Trie (Prefix Tree)](7%20-%20Tree/Trie.md): Efficient insert/search/startsWith for strings
- [Union-Find or Disjoint Set Union](7%20-%20Tree/Union-Find.md)
- [Segment Tree](7%20-%20Tree/Segment%20Tree.md)
- [Fenwick Tree (Binary Indexed Tree)](7%20-%20Tree/Fenwick%20Tree.md)
- [Heap](7%20-%20Tree/Heap%20Tree.md),
- [Suffix Tree/Array](7%20-%20Tree/Suffix%20Tree.md)

# <h1 align=center>Graph</h1>

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

# <h1 align=center>Sorting</h1>

1. [**Bubble Sort**](6%20-%20Sorting/Bubble%20Sort.md): Compare and swap adjacent elements. O(N²)
2. [**Selection Sort**](6%20-%20Sorting/Selection%20Sort.md): Select min and swap with start. O(N²)
3. [**Insertion Sort**](6%20-%20Sorting/Insertion%20Sort.md): Insert key in sorted part. O(N²)
4. [**Merge Sort**](6%20-%20Sorting/Merge%20Sort.md): Divide and merge. O(NlogN)
5. [**Quick Sort**](6%20-%20Sorting/Quick%20Sort.md): Partition around pivot. O(NlogN) average
6. [**Counting Sort**](6%20-%20Sorting/Counting%20Sort.md): Count occurrences. O(N+K), only for positive numbers
7. [**Heap Sort**](6%20-%20Sorting/Heap%20Sort.md): Build heap, extract max/min. O(NlogN)

# <h1 align=center>Searching</h1>

1. **Linear Search**
2. **Binary Search**

# <h1 align=center>Greedy Algorithm</h1>

- Approach: Make the best choice at each step; may not be globally optimal.
- Properties: Greedy choice property, optimal substructure
- Examples: Selection Sort, Knapsack, MST, Job Scheduling, Dijkstra, Huffman Coding, Ford-Fulkerson

# <h1 align=center>Dynamic Programming</h1>

- Efficient for overlapping subproblems and optimal substructure.
- Store solutions to subproblems to avoid recomputation.
- Examples: Floyd-Warshall, Longest Common Subsequence, 0/1 Knapsack, Palindromes

# <h1 align=center>Extra algorithms</h1>

- Backtracking
- Rabin-Karp (Rolling Hash)
- Knuth-Morris-Pratt (KMP)
- Boyer-Moore (Majority Voting)

---

## <h1 align=center>Useful Links</h1>

- https://seanprashad.com/leetcode-patterns/
- https://github.com/hxu296/leetcode-company-wise-problems-2022
- https://www.programiz.com/dsa
- https://www.geeksforgeeks.org/c-program-to-print-all-permutations-of-a-given-string-2/
