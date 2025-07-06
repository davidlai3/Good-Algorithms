
```cpp
class Trie {
private:

	struct TrieNode {
		// pointer array for child nodes of each node
		TrieNode* child[26];
		// Used for indicating ending of string
		bool wordEnd;
		TrieNode() {
			wordEnd = false;
			for (int i = 0; i < 26; i++) {
				child[i] = NULL;
			}
		}
	};

	TrieNode *root;

public:
	Trie() {
		root = new TrieNode();
	}

	void insert(string word) {
		TrieNode* curr = root;
		for (char c : word) {
			// Check if the node exists for the
			// current character in the Trie
			if (curr->child[c - 'a'] == nullptr) {
				// If node for current character does
				// not exist then make a new node
				TrieNode* newNode = new TrieNode();
				// Keep the reference for the newly
				// created node
				curr->child[c - 'a'] = newNode;
			}
			// Move the curr pointer to the
			// newly created node
			curr = curr->child[c - 'a'];
		}
		curr->wordEnd = true;
	}

	bool search(string word) {
		// Initialize the curr pointer with the root node
		TrieNode* curr = root;
		// Iterate across the length of the string
		for (char c : word) {
			// Check if the node exists for the
			// current character in the Trie
			if (curr->child[c - 'a'] == nullptr)
			return false;
			// Move the curr pointer to the
			// already existing node for the
			// current character
			curr = curr->child[c - 'a'];
		}
		// Return true if the word exists
		// and is marked as ending
		return curr->wordEnd;
	}

	bool startsWith(string prefix) {
		TrieNode* curr = root;
		for (char c : prefix) {
			if (curr->child[c - 'a'] == nullptr)
				return false;
			curr = curr->child[c-'a'];
		}
		return true;
	}
};
```