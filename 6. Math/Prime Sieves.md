## Sieve of Eratosthenes
- Time Complexity: $O(n\log\log n)$
	- For more on this, visit https://www.geeksforgeeks.org/how-is-the-time-complexity-of-sieve-of-eratosthenes-is-nloglogn/
- Space Complexity: $O(n)$
```cpp
vector<int> generatePrimes(int n) { 
	vector<bool> isPrime(n + 1, true); 
	isPrime[0] = isPrime[1] = false; 
	for (int i = 2; i * i <= n; ++i) { 
		if (isPrime[i]) { 
			for (int j = i * i; j <= n; j += i) {
				isPrime[j] = false; 
			} 
		} 
	} 

	vector<int> primes;
	for (int i = 2; i <= n; ++i) { 
		if (isPrime[i]) { 
			primes.pb(i);
		}
	}
	return primes;
} 
```
### Segmented Sieves
- Sometimes we want to sieve only on some range $[l, r]$. A naive solution is to just sieve on the range $[0, r]$ and truncate the left side of the array, but there is a better way to do this.
```cpp
vector<int> segmented_sieve(int l, int r) {
	if (l < 2) l = 2;
	int limit = sqrt(r);
	vector<int> primes = generatePrimes(limit);
	vector<bool> prime_range(r-l+1, true);

	for (int p : primes) {
		// find first multiple of p in range
		int start = max(p * p, (l + p - 1) / p * p);

		for (int j = start; j < r+1; j += p) {
			prime_range[j-l] = false;
		}
	}
	vector<int> segmented_primes;
	for (int i = 0; i < r-l+1; i++) {
		if (prime_range[i]) segmented_primes.pb(l+i);
	}
	return segmented_primes;
}
```