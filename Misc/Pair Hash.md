```cpp
struct PairHash {
	std::size_t operator()(const std::pair<int, int>& p) const noexcept {
		// 64‑bit mix: shift the first int up and XOR‑fold in the second
		return (static_cast<std::size_t>(static_cast<uint32_t>(p.first)) << 32)
			^  static_cast<uint32_t>(p.second);
	}
};
```