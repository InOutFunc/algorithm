## 76. Minimum Window Substring

```cpp
class Solution {
public:
    string minWindow(string s, string t) {
        unordered_map<char, int> chars;
        for (const auto& item : t) {
            chars[item]++;
        }
        
        int l = 0;
        int r = 0;
        int minL = 0;
        int minR = INT_MAX;
        int counter = chars.size();
        while (r < s.size()) {
            if (chars.find(s[r]) == chars.end()) {
                r++;
                continue;
            }
            if (chars[s[r]] == 1) {
                counter--;
            }
            chars[s[r]]--;
            while (counter == 0) {
                if (r - l < minR - minL) {
                    minL = l;
                    minR = r;
                }
                if (chars.find(s[l]) == chars.end()) {
                    l++;
                    continue;
                }
                if (chars[s[l]] == 0) {
                    counter++;
                }
                chars[s[l]]++;
                l++;
            }
            r++;
        }
        if (minR == INT_MAX) {
            return "";
        }
        return s.substr(minL, minR - minL + 1);
    }
};
```

