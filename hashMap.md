## 41. First Missing Positive

```cpp
class Solution {
public:
    int firstMissingPositive(vector<int>& nums) {
        for (int i = 0; i < nums.size(); i++) {
            while (nums[i] >= 1 && nums[i] <= nums.size() && nums[i] != nums[nums[i] - 1]) {
                swap(nums[i], nums[nums[i] - 1]);
            }
        }
        
        for (int i = 0; i < nums.size(); i++) {
            if (nums[i] != i + 1) {
                return i + 1;
            }
        }
        
        return nums.size() + 1;
    }
};
```

## 347. Top K Frequent Elements

```cpp
class Solution {
public:
    vector<int> topKFrequent(vector<int>& nums, int k) {
        unordered_map<int, int> counter;
        for (int num : nums) {
            counter[num]++;
        }
        int n = nums.size();
        vector<vector<int>> buckets(n + 1);
        for (auto& kv : counter) {
            buckets[kv.second].push_back(kv.first);
        }
        vector<int> res;
        for (int i = n; i >= 0; i--) {
            for (int j = 0; j < buckets[i].size(); j++) {
                res.push_back(buckets[i][j]);
                if (res.size() == k) {
                    return res;
                }
            }
        }
        return {};
    }
};
```

## 448. Find All Numbers Disappeared in an Array

```cpp
class Solution {
public:
    vector<int> findDisappearedNumbers(vector<int>& nums) {
        for (int i = 0; i < nums.size(); i++) {
            nums[abs(nums[i]) - 1] = -abs(nums[abs(nums[i]) - 1]);
        }
        vector<int> res;
        for (int i = 0; i < nums.size(); i++) {
            if (nums[i] > 0) {
                res.push_back(i + 1);
            }
        }
        return res;
    }
};
```

