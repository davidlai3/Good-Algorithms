## Overview (0/1 Version)
- There are many ways a knapsack problem can be defined, but typically it is in the form: What is the maximum/minimum amount of $x$ you can get with some restriction $y$?
- Here's an example:
	- You are in a book shop which sells $n$ different books. You know the price and number of pages of each book.
	- You have decided that the total price of your purchases will be at most $m$. What is the maximum number of pages you can buy? You can buy each book at most once.
- Time Complexity: $O(n*m)$
- Space Complexity: $O(n*m)$

## Approach
1. Let's define a 2D array called $dp[i][j]$, where there are $n$ rows and $m$ columns
2. $dp[i][j]$ will represent the maximum number of pages you can buy using the first $i$ books and spending at most $j$ dollars
3. As we iterate over the table, we consider the choice to buy the $i$th book. Thus, our recurrence is $$dp[i][j] = \max(dp[i-1][j], dp[i-1][j-cost[i]] + pages[i])$$

## Implementation
```cpp
// dp[i][j] = maximum number of pages you can buy using first i books and spending at most j dollars
int dp[M][N];
    
void sol() {
	int n, x; cin >> n >> x;
	// h[i] = price of book i
	// s[i] = pages in book i
	vector<int> h(n+1), s(n+1);
	for (int i = 1; i <= n; i++) cin >> h[i];
	for (int i = 1; i <= n; i++) cin >> s[i];
 
	for (int i = 1; i <= n; i++) {
		for (int j = 1; j <= x; j++) {
			if (h[i] > j) dp[i][j] = dp[i-1][j];
			else dp[i][j] = max(dp[i-1][j], dp[i-1][j-h[i]] + s[i]);
		}
	}
 
	cout << dp[n][x] << endl;
}

```