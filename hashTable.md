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

## 121. Best Time to Buy and Sell Stock

```cpp
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int curMin = prices[0];
        int res = 0;
        for (int i = 1; i < prices.size(); i++) {
            res = max(res, prices[i] - curMin);
            curMin = min(curMin, prices[i]);
        }
        return res;
    }
};
```

## 128. Longest Consecutive Sequence

```cpp
class Solution {
public:
    int longestConsecutive(vector<int>& nums) {
        unordered_set<int> numSet(nums.begin(), nums.end());
        int res = 0;
        for (int i = 0; i < nums.size(); i++) {
            if (numSet.find(nums[i] - 1) != numSet.end()) {
                continue;
            }
            int count = 1;
            while (numSet.find(nums[i] + count) != numSet.end()) {
                count++;
            }
            res = max(res, count);
        }
        return res;
    }
};
```

