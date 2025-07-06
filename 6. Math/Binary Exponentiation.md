- $O(\log n)$ exponentiation
```c++
long long binpow(long long a, long long b) {
	if (b == 0)
		return 1;
	long long res = binpow(a, b / 2);
	res = (res * res) % mod;
	if (b % 2) {
		res = (res * a) % mod;
	}
	return res;
}
```