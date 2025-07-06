## Overview
- Range DP's are used to find optimal solutions over a certain range $[i, j]$. They are most commonly used when asked to find optima over an entire array given some transition that is dependent on previous ranges
- Typically, if we are working with range DPs, our overall goal would be to find an optimal solution over an entire array. Thus, we tend to start iterating from position $[n, n]$, where $n$ is the length of the array
- Time: At least $O(n^2)$
- Space: $O(n^2)$

## Approach
Consider the following problem:
- There is a list of n numbers and two players who move alternately. On each move, a player removes either the first or last number from the list, and their score increases by that number. Both players try to maximize their scores.
- What is the maximum possible score for the first player when both players play optimally?

1. Let's define a 2D array called $dp[i][j]$, where $dp[i][j]$ represents the maximum score difference between players 1 and 2
2. Starting from the bottom right, we build up our DP table
3. If $[i, j]$ only contains one element, then the maximum score difference must be $a[i]$
4. However, if $[i, j]$ contains multiple elements, then we can use our previous DP values:$$dp[i][j]=max(a[i] - dp[i+1][j], a[i]-dp[i][j-1])$$
5. The above equation works because at each new element added, we can either remove the left side or the right side. After this, we already have the optimal solution for the newly created array.
## Implementation
```cpp
ll dp[N][N];

void sol() {
	int n; cin >> n;
	vector<int> a(n+1, 0);
	ll total = 0;
	for (int i = 1; i <= n; i++) {
		int x; cin >> x;
		a[i] = x; total += x;
	}

	for (int i = n; i >= 1; i--) {
		for (int j = i; j <= n; j++) {
			if (i == j) {
				dp[i][j] = a[i];
				continue;
			}
			// take left side vs take right side
			dp[i][j] = max(a[i] - dp[i+1][j], a[j] - dp[i][j-1]);
		}
	}

	cout << (total - dp[1][n])/2 + dp[1][n] << endl;
}
```