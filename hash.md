## 49. Group Anagrams

```cpp
class Solution {
public:
    vector<vector<string>> groupAnagrams(vector<string>& strs) {
        unordered_map<string, vector<string>> words;
        for (const auto& str : strs) {
            string tmp = str;
            sort(tmp.begin(), tmp.end());
            words[tmp].push_back(str);
        }
        
        vector<vector<string>> res;
        for (const auto& kv : words) {
            res.push_back(kv.second);
        }
        
        return res;
    }
};
```