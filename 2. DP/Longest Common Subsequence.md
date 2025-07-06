## Overview
- The longest common subsequence problem asks to find the longest common subsequence of elements given two sequences $X$ and $Y$.
- Time: $O(mn)$
- Space: $O(mn)$
## Recurrence
- Notice how similar this recurrence is to the recurrence for the [[Levenshtein Distance]].
$$dp[i][j] = \begin{cases}
0 & (i = 0)\lor(j=0) \\
1 + dp[i-1][j-1] & (i, j > 0) \land (X[i] = Y[j]) \\
\max(dp[i-1][j], dp[i][j-1]) & (i,j > 0) \land (X[i] \neq Y[j])
\end{cases}$$
## Implementation
```cpp
void lcs() {
	int n, m; cin >> n >> m;
	vector<int> x(n+1), y(m+1);
	for (int i = 1; i <= n; i++) {
		cin >> x[i];
	}
	for (int i = 0; i <= m; i++) {
		cin >> y[i]
	}
	for (int i = 1; i <= n; i++) {
		for (int j = 1; j <= m; j++) {
			if (x[i] == y[j]) {
				dp[i][j] = 1 + dp[i-1][j-1];
			}
			else {
				dp[i][j] = max(dp[i-1][j], dp[i][j-1]);
			}
		}
	}
	cout << dp[n][m] << endl;
}
```
