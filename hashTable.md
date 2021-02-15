## 1. Two Sum

```cpp
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        unordered_map<int, int> adds;
        for (int i = 0; i < nums.size(); i++) {
            auto iter = adds.find(target - nums[i]);
            if (iter != adds.end()) {
                return {i, iter->second};
            }
            adds[nums[i]] = i;
        }
        
        return {};
    }
};
```

## 3. Longest Substring Without Repeating Characters

```cpp
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        int l = 0;
        int r = 0;
        int res = 0;
        unordered_map<char, int> lefts;
        while (r < s.size()) {
            auto iter = lefts.find(s[r]);
            if (iter != lefts.end()) {
                l = max(l, iter->second + 1);
            }
            res = max(res, r - l + 1);
            lefts[s[r]] = r;
            r++;
        }
        
        return res;
    }
};
```

