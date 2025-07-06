`begin()`: This function is used to return the beginning position of the container (i.e. first element in a vector).
`end()`: This function is used to return the after end position of the container (i.e. after the last element of a vector).
`rbegin():` This function is used to return the end position of the container (i.e. the last element of a vector)
```cpp
#include<iostream> 
#include<iterator> // for iterators 
#include<vector> // for vectors 
using namespace std; 
int main() 
{ 
    vector<int> ar = { 1, 2, 3, 4, 5 }; 
      
    // Declaring iterator to a vector 
    vector<int>::iterator ptr; 
      
    // Displaying vector elements using begin() and end() 
    cout << "The vector elements are : "; 
    for (ptr = ar.begin(); ptr != ar.end(); ptr++) 
        cout << *ptr << " "; 
      
    return 0;     
} 
```

`advance()`: This function is used to increment the iterator position till the specified number mentioned in its arguments.
```cpp
#include<iostream> 
#include<iterator> // for iterators 
#include<vector> // for vectors 
using namespace std; 
int main() 
{ 
    vector<int> ar = { 1, 2, 3, 4, 5 }; 
      
    // Declaring iterator to a vector 
    vector<int>::iterator ptr; 

	advance(ptr, 3);
      
    return 0;     
} 
```

`next()`: This function returns the new iterator that the iterator would point after advancing the positions mentioned in its arguments.
`prev()`: This function returns the new iterator that the iterator would point after decrementing the positions mentioned in its arguments.
Note: Trying to call `next()` on `vector.end()` or `prev()` on `vector.begin()` leads to undefined behavior. Check the iterator you are calling this on for safety.

```cpp
#include<iostream> 
#include<iterator> // for iterators 
#include<vector> // for vectors 
using namespace std; 
int main() 
{ 
    vector<int> ar = { 1, 2, 3, 4, 5 }; 
      
    // Declaring iterators to a vector 
    vector<int>::iterator ptr = ar.begin(); 
    vector<int>::iterator ftr = ar.end(); 
     
     
    // Using next() to return new iterator 
    // points to 4 
    auto it = next(ptr, 3); 
      
    // Using prev() to return new iterator 
    // points to 3 
    auto it1 = prev(ftr, 3); 
}
```

`inserter()`: This function is used to insert the elements at any position in the container. It accepts 2 arguments, the container and iterator to position where the elements have to be inserted.
```cpp
#include<iostream> 
#include<iterator> // for iterators 
#include<vector> // for vectors 
using namespace std; 
int main() 
{ 
    vector<int> ar = { 1, 2, 3, 4, 5 }; 
    vector<int> ar1 = {10, 20, 30};  
      
    // Declaring iterator to a vector 
    vector<int>::iterator ptr = ar.begin(); 
     
    // Using advance to set position 
    advance(ptr, 3); 
      
    // copying 1 vector elements in other using inserter() 
    // inserts ar1 after 3rd position in ar 
    copy(ar1.begin(), ar1.end(), inserter(ar,ptr)); 
}
```