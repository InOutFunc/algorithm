## 208. Implement Trie (Prefix Tree)

```cpp
class TrieNode {
public:
    vector<TrieNode*> nodes = vector<TrieNode*>(26);
    bool isWord;
    TrieNode()
    {
        for (int i = 0; i < nodes.size(); i++) {
            nodes[i] = nullptr;
        }
        isWord = false;
    }
};
class Trie {
public:
    /** Initialize your data structure here. */
    Trie() {
        
    }
    
    /** Inserts a word into the trie. */
    void insert(string word) {
        TrieNode* p = root;
        for (const auto& item : word) {
            int i = item - 'a';
            if (p->nodes[i] == nullptr) {
                p->nodes[i] = new TrieNode();
            }
            p = p->nodes[i];
        }
        p->isWord = true;
    }
    
    /** Returns if the word is in the trie. */
    bool search(string word) {
        TrieNode* p = root;
        for (const auto& item : word) {
            int i = item - 'a';
            if (p->nodes[i] == nullptr) {
                return false;
            }
            p = p->nodes[i];
        }
        return p->isWord;
    }
    
    /** Returns if there is any word in the trie that starts with the given prefix. */
    bool startsWith(string prefix) {
        TrieNode* p = root;
        for (const auto& item : prefix) {
            int i = item - 'a';
            if (p->nodes[i] == nullptr) {
                return false;
            }
            p = p->nodes[i];
        }
        return true;
    }
private:
    TrieNode* root = new TrieNode();
};

/**
 * Your Trie object will be instantiated and called as such:
 * Trie* obj = new Trie();
 * obj->insert(word);
 * bool param_2 = obj->search(word);
 * bool param_3 = obj->startsWith(prefix);
 */
```

