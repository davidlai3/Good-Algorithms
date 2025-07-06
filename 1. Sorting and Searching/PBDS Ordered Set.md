Ordered set is a policy based data structure in g++ that keeps the **unique** elements in sorted order. It performs all the operations as performed by the set data structure in STL in $\log(n)$ complexity and performs two additional operations also in $\log(n)$ complexity :
- `order_of_key(int k)` : Number of items strictly smaller than k .
- `find_by_order(int k)` : K-th largest element in a set (counting from zero).
Both of these functions run in $O(\log n)$, where $n$ is the size of the set.

- Note: If you want to use a multiset instead, change `std::less<T>` argument to `std::less_equal<T>`.  Note that a drawback of this is that `lower_bound` works as `upper_bound`.

```cpp
#include <ext/pb_ds/assoc_container.hpp>
#include <ext/pb_ds/tree_policy.hpp>
using namespace __gnu_pbds;

template <typename T>
using ordered_set = tree<T, null_type, std::less<T>, rb_tree_tag, tree_order_statistics_node_update>;

int main() {
    ordered_set<int> os;
    os.insert(10);
    os.insert(20);
    os.insert(30);

    // Index-based access
    std::cout << *os.find_by_order(1) << "\n"; // Prints 20
}
```