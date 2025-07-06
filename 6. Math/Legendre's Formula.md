## Overview
Legendre's Formula states that: $$\nu_{p}(n!)= \sum_{i=1}^{\infty} \left\lfloor \frac{n}{p^i} \right\rfloor$$
This formula gives us the number of times some prime $p$ appears in the factorization $n!$.
## Alternative Form
Another equivalent definition of Legendre's Formula is: $$\nu_{p}(n!) = \frac{n - S_p(n)}{p-1}$$
where $S_p(n)$ is the base $p$ representation of $n$.
## Implementation
```cpp
int leg(int n, int p)  { 
    int res = 0; 
    while (n > 0) { 
        n /= p; 
        res += n; 
    } 
    return res; 
} 
```