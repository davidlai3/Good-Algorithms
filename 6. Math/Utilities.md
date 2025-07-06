## Primality Test
- Time: $O(\sqrt{n})$
- Space: $O(1)$
```cpp
bool is_prime(ll n) {
    if(n < 2) return false;
    if(n == 2) return true;
    if(n % 2 == 0) return false;
    for(ll i = 3; (i*i) <= n; i+=2){
        if(n % i == 0) return false;
    }
    return true;
}
```
## Prime Factorization Generator
- Time: $O(\sqrt{n})$
- Space: $O(1)$
```cpp
vector<pair<ll, ll>> get_primes(ll n) {
	vector<pair<ll, ll>> factors;

    ll count = 0;
    while (n % 2 == 0) {
        count++;
        n /= 2;
    }
    if (count > 0) {
        factors.push_back({2, count});
    }

    for (ll i = 3; i <= ceil(sqrt(n)); i += 2) {
        count = 0;
        while (n % i == 0) {
            count++;
            n /= i;
        }
        if (count > 0) {
            factors.push_back({i, count});
        }
    }

    if (n > 2) {
        factors.push_back({n, 1});
    }

    return factors;
}
```
## Fast Exponentiation
```c++
long long fastExpRec(long long base, long long exponent, long long mod) {
    if (exponent == 0) return 1;
    long long half = fastExpRec(base, exponent / 2, mod);
    long long res = (half * half) % mod;
    if (exponent % 2 == 1) {
        res = (res * base) % mod;
    }
    return res;
}
```

## Extended Euclidean Algorithm
```cpp
bool is_coprime(int x, int y) {

	gcd(x, y) = gcd(x, x % y);
}
```