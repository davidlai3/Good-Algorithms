In C++, type casting is a way to convert one data type to another. There are different kinds of casts with specific use cases.

## C-Style Cast
- Syntax: `(new type) expression`
- This is the traditional casting syntax from C. It's dangerous because it performs different types of casts (like `static_cast`, `const_cast`, or even `reinterpret cast`) depending on the situation.
- Use Case: 
	- Simple and quick, but lacks clarity and safety. Should be avoided in favor of more specific cast operators.

## Static Cast
- Syntax: `static_cast<new_type>(expression)`
- This is the most common cast in C++. It is used for converting between related types (e.g., bases and derived classes, or between numeric types). It performs a compile-time check to ensure that the types are compatible but **does not check if the cast is safe at runtime**.
- Use Case:
	- Casting between fundamental types (e.g., `int` to `double`)
	- Casting pointers/references between related types in inheritance
	- Used when you know that the cast is valid and safe

## Dynamic Cast
- Syntax: `dynamic_cast<new_type>(expression)`
- This cast is used exclusively with pointers or references to polymorphic types (i.e., types that have virtual functions). It performs runtime checks to ensure the validity of the cast. If the cast is not valid, it returns `nullptr` for pointers and throws an exception for references.
- Use Case:
	- Safe downcasting in a class hierarchy.
	- Used when you are not sure whether the cast will succeed and you want a **runtime check**.