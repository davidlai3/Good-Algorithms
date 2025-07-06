## Point Structure
```cpp
typedef double T;
struct pt {
	T x,y;
	pt operator+(pt p) {return {x+p.x, y+p.y};}
	pt operator-(pt p) {return {x-p.x, y-p.y};}
	pt operator*(T d) {return {x*d, y*d};}
	pt operator/(T d) {return {x/d, y/d};} // only for floating point
	bool operator==(pt p) {return x == p.x && y == p.y;}
	bool operator!=(pt p) {return x != p.x || y != p.y;}
	T sq(pt p) {return p.x*p.x + p.y*p.y;}
	double abs(pt p) {return sqrt(sq(p));}
}
```