## Overview
An increasing subsequence $L$ of a given sequence $A = \langle a_{1}, a_{2}, \dots a_{n}\rangle$ is obtained by deleting zero or more numbers from $A$ such that every number $x \in L$ is larger than the number immediately preceding $x$ in $L$.
- Time: $O(n^2)$
## Recurrence
Our recurrence is defined as:
$$dp[i] = 1 + \max_{0 \leq j < i}\{dp[j] | a_{j} > a_{i}\}$$
Where $dp[i]$ is the length of the longest increasing subsequence that ends at $i$.
## Implementation
```cpp
int dp[N];

void lis() {
	int n; cin >> n;
	vector<int> a(n+1);
	a[0] = INT_MIN;
	for (int i = 1; i <= n; i++) {
		cin >> a[i];
	}

	dp[0] = 0;
	for (int i = 1; i <= n; i++) {
		for (int j = 0; j < i; j++) {
			if (a[i] > a[j]) {
				dp[i] = max(dp[i], 1 + dp[j]);
			}
		}
	}
	cout << *max_element(dp, dp+n); << endl;
}
```
