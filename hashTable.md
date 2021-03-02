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

## 560. Subarray Sum Equals K

```cpp
class Solution {
public:
    int subarraySum(vector<int>& nums, int k) {
        unordered_map<int, int> preSum;
        preSum[0] = 1;
        int sum = 0;
        int res = 0;
        for (int i = 0; i < nums.size(); i++) {
            sum += nums[i];
            if (preSum.find(sum - k) != preSum.end()) {
                res += preSum[sum - k];
            }
            preSum[sum]++;
        }
        return res;
    }
};
```

## 581. Shortest Unsorted Continuous Subarray

```cpp
class Solution {
public:
    int findUnsortedSubarray(vector<int>& nums) {
        int curMax = INT_MIN;
        int r = -1;
        for (int i = 0; i < nums.size(); i++) {
            if (nums[i] < curMax) {
                r = i;
                continue;
            }
            curMax = nums[i];
        }
        
        int l = -1;
        int curMin = INT_MAX;
        for (int i = nums.size() - 1; i >= 0; i--) {
            if (nums[i] > curMin) {
                l = i;
                continue;
            }
            curMin = nums[i];
        }
        
        if (r == -1 && l == -1) {
            return 0;
        }
        return r - l + 1;
    }
};
```

## 739. Daily Temperatures

```cpp
class Solution {
public:
    vector<int> dailyTemperatures(vector<int>& T) {
        stack<int> pre;
        vector<int> res(T.size());
        for (int i = 0; i < T.size(); i++) {
            while (!pre.empty() && T[i] > T[pre.top()]) {
                int cur = pre.top();
                pre.pop();
                res[cur] = i - cur;
            }
            pre.push(i);
        }
        res[T.size() - 1] = 0;
        return res;
    }
};
```

## 437. Path Sum III

```cpp
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    int pathSum(TreeNode* root, int sum) {
        unordered_map<int, int> preSum;
        preSum[0] = 1;
        return divide(root, 0, sum, preSum);
    }
private:
    int divide(TreeNode* root, int curSum, int sum, unordered_map<int, int>& preSum)
    {
        if (root == nullptr) {
            return 0;
        }
        curSum += root->val;
        int res = 0;
        if (preSum.find(curSum - sum) != preSum.end()) {
            res += preSum[curSum - sum];
        }
        preSum[curSum]++;
        res += divide(root->left, curSum, sum, preSum) + divide(root->right, curSum, sum, preSum);
        preSum[curSum]--;
        return res;
    }
};
```

