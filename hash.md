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

## jz34 第一个只出现一次的字符

```cpp
#include <unordered_map>
class Solution {
public:
    int FirstNotRepeatingChar(string str) {
        unordered_map<char, int> charCnt;
        for (const auto item : str) {
            charCnt[item]++;
        }
        for (int i = 0; i < str.size(); i++) {
            if (charCnt[str[i]] == 1) {
                return i;
            }
        }
        
        return -1;
    }
};
```

