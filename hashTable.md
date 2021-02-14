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

```

