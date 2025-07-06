## Overview
- The Levenshtein distance, or edit distance, is the value that represents the distance between two strings. In other words, it is a measure of the minimum number of operations required to transform some string $s_1$ into $s_2$
	- The allowed operations are addition of a character, removal of a character, and replacement of a character

## Approach
1. Let's define a 2D array as $dp[i][j]$, where there are $len(s_1)+1$ rows and $len(s_2)+1$ cols
2. $dp[i][j]$ will represent the number of operations required to go from $s_1[0:i]$ to $s_2[0:j]$
3. To start, $dp[0][i]=0,1,2,\ldots,len(s_1)$ and $dp[i][0]=0,1,2,\ldots,len(s_2)$. This makes sense because it requires $k$ operations to get the first $k$ characters of a string starting from an empty string
4. How do we populate our dp?
	1. If $s_{1}[i] \neq s_{2}[j]$, then $dp[i][j]=1 + min(dp[i-1][j], dp[i][j-1], dp[i-1][j-1])$
	2. If $s_{1}[i] = s_{2}[j]$, then $dp[i][j]=dp[i-1][j-1]$
5. This makes sense because in the first case, $dp[i][j]$ can be reached from each of the positions inside the $min$ function. In the second case, going to $dp[i][j]$  requires no operation because the characters are already the same
6. The result is stored in $dp[len(s_1)][len(s_2)]$

## Implementation
- Note: I differentiated the strings here by the shorter and longer one, but I don't think it actually matters how you do it
```cpp
	vector<vector<int>> dp(mn_len+1, vector<int>(mx_len+1, 0));
 
	for (int i = 0; i <= mx_len; i++) {
		dp[0][i] = i;
	}
	for (int i = 0; i <= mn_len; i++) {
		dp[i][0] = i;
	}
 
	for (int i = 1; i <= mn_len; i++) {
		for (int j = 1; j <= mx_len; j++) {
			int l = dp[i][j-1];
			int u = dp[i-1][j];
			int d = dp[i-1][j-1];
			if (mx_str[j-1] == mn_str[i-1]) {
				dp[i][j] = d;
			}
			else {
				dp[i][j] = 1 + min3(l, u, d);
			}
		}
	}

	cout << dp[mn_len][mx_len] << endl;

```
