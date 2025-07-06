In C++, the `auto` keyword is used to automatically deduce the type of a variable based on the value it is initialized with. This helps make code more concise and easier to read, especially when dealing with complex types.

## Properties of Auto
### Type Deduction
When you declare a variable using `auto`, the compiler infers its type from the initializer. For example,
```cpp
auto x = 5;     // deduced as int
auto y = 3.14;  // deduced as double
```
### Works with Expressions
`auto` can be used for more complex types or expressions
```cpp
auto z = x + y // z = is deduced as a double
```
### Use with Iterators
`auto` is often helpful when we are working with complex or verbose types 
```cpp
std::vector<int> vec = {1, 2, 3};
auto it = vec.begin(); // auto represents std::vector<int>::iterator
```
###  Lambdas
`auto` is also helpful when using lambdas or function pointers, where the type can be complex.
```cpp
auto lambda = [](int a, int b) {return a + b; };
```
### Const and References
`auto` can be combined with const and reference qualifiers
```cpp
const auto &ref = x; // ref is a constant reference to an int;
```
### Limitations
`auto` requires an initializer, so it cannot be used for uninitialized  variables. You cannot write:
```cpp
auto x; // Error
```