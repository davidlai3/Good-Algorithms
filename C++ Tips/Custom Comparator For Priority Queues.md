```cpp
struct compare {
	bool operator()(const int &a, const int &b) {
		return a > b; // min heap
	}
}

priority_queue<int, vector<int>, compare> pq;
```