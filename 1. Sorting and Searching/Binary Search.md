## Overview
- Given a sorted collection of elements, binary search allows us to find whether or not an element exists in $O(\log n)$ time
- Very flexible implementation and open to many variations
## Implementation

Classic Implementation
```cpp
int binary_search(vector<int> nums, int target):
	int l = 0, r = nums.size() - 1;

	while (l <= r):
		int mid = (l+r) >> 1;
		if (target == nums[mid])
			return mid;
		elif (target > nums[mid])
			left = mid+1;
		else: 
			right = mid-1;

	return -1;
```
- After this loop is over, if the target is not found then the left pointer points to the first element greater than or equal to the target, while the right pointer points to the first element less than or equal to the target.

Decreasing then Increasing (Bitonic)
```cpp
int minimal(int a[], int n) {
    int lo = 0, hi = n - 1;
    // Do a binary search
    while (lo < hi) {
        // Find the mid element
        int mid = (lo + hi) >> 1;
        // Check for break point
        if (a[mid] < a[mid + 1]) {
            hi = mid;
        }
        else {
            lo = mid + 1;
        }
    }
    // Return the index
    return lo;
}
```

Using a check function
```cpp
bool check(vector<int> &piles, int speed, int h) {
	long long ans = 0;
	for (int n : piles) {
		ans += (long long) (n + speed - 1) / speed;
	}
	return ans <= h;
}
int binary_search(vector<int>& piles, int h) {
	int l = 1;
	int r = *max_element(piles.begin(), piles.end());

	while (l <= r) {
		int mid = (l + r) >> 1;
		if (check(piles, mid, h)) {
			r = mid-1;
		}
		else {
			l = mid+1;
		}
	}
	return l;
}
```

## Built-In Library Functions
- The C++ `<algorithm>` library provides us with built-in binary search functions.
- `lower_bound` finds the first position in a sorted range that is not less than a given value.
- `upper_bound` finds the first position in a sorted range that is strictly greater than a given value.
- If all elements in the container are less than the target value, then the functions return an end iterator.
- For containers that are intrinsically sorted like `set` or `map`, the functions are seamless.
## Example
```cpp
#include <iostream>
#include <vector>
#include <algorithm>

int main() {
    vector<int> vec = {10, 20, 30, 30, 40, 50};
    int value = 30;

    // Finding lower bound
    auto lb = lower_bound(vec.begin(), vec.end(), value);
    cout << "Lower bound of " << value << " is at index: " 
              << (lb - vec.begin()) << "\n"; // Prints idx of first 30

    // Finding upper bound
    auto ub = upper_bound(vec.begin(), vec.end(), value);
    cout << "Upper bound of " << value << " is at index: " 
              << (ub - vec.begin()) << "\n"; // Prints idx of 40 

    std::set<int> s = {10, 20, 30, 40, 50};

    // Finding lower and upper bounds
    auto lb_set = s.lower_bound(value);
    auto ub_set = s.upper_bound(value);

    return 0;
}
```

