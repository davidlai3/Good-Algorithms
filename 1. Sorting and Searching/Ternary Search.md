## Overview
- Ternary search is a variation of binary search, typically used to search for elements in **bitonic** sequences or evaluating quadratic expressions.
- Time: $O(2*log_{3}n)$
- Space: $O(log_{3}n)$

## Approach
1. Initialize
	- Set two pointers, left and right, initially pointing to the first and last elements of our search space
2. Divide the search space
	- Calculate two midpoints, `mid1` and `mid2`, dividing the current search space into 3 parts
	- The array is now divided into `[left, mid1]`, `(mid1, mid2)`, and `[mid2, right]`
4. Compare with target 
	- If the target is equal to the element at `mid1` or `mid2`, the search is successful
	- If the target is less than the element at `mid1`, update the right pointer to `mid1-1`
	- If the target is greater than the element at `mid2`, update the left pointer to `mid2+1`
	- If the target is between `mid1` and `mid2`, update left to `mid1+1` and right to `mid2-1`
5. Repeat

```cpp
int ternarySearch(int l, int r, int key, int ar[])
{
    if (r >= l) {

        // Find the mid1 and mid2
        int mid1 = l + (r - l) / 3;
        int mid2 = r - (r - l) / 3;

        // Check if key is present at any mid
        if (ar[mid1] == key) {
            return mid1;
        }
        if (ar[mid2] == key) {
            return mid2;
        }

		// check region 1
        if (key < ar[mid1]) {
            return ternarySearch(l, mid1 - 1, key, ar);
        }
		// check region 2
        else if (key > ar[mid2]) {
            return ternarySearch(mid2 + 1, r, key, ar);
        }
		// check region 3
        else {
            return ternarySearch(mid1 + 1, mid2 - 1, key, ar);
        }
    }

    // Key not found
    return -1;
}
```