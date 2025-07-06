## Overview
- Oftentimes, it is possible to determine the intended time complexity of a solution by looking at the constraints
	
|  Constraints  | Worst Time Complexity |            Algorithmic Solution            |
| :-----------: | :-------------------: | :----------------------------------------: |
|  $n \leq 12$  |        $O(n!)$        |    $\text{Recursion and Backtracking}$     |
|  $n \leq 25$  |       $O(2^n)$        |       Backtracking, Bit manipulation       |
| $n \leq 100$  |       $O(n^4)$        |     Backtracking, Dynamic Programming      |
| $n \leq 500$  |       $O(n^3)$        |            Dynamic Programming             |
| $n \leq 10^4$ |       $O(n^2)$        |     Dynamic Programming, Graphs, Trees     |
| $n \leq 10^6$ |     $O(n \log n)$     | Sorting, Binary Search, Divide and Conquer |
| $n \leq 10^8$ |        $O(n)$         |            Mathematical, Greedy            |
|  $n > 10^8$   |   $O(\log n), O(1)$   |            Mathematical, Greedy            |
