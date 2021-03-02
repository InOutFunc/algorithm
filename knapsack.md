## 322. Coin Change

```cpp
// class Solution {
// public:
//     int coinChange(vector<int>& coins, int amount) {
//         int n = coins.size();
//         vector<vector<int>> dp(n + 1, vector<int>(amount + 1, amount + 1));
//         for (int i = 0; i < n + 1; i++) {
//             dp[i][0] = 0;
//         }
//         for (int i = 1; i < n + 1; i++) {
//             for (int j = 1; j < amount + 1; j++) {
//                 if (j >= coins[i - 1]) {
//                     dp[i][j] = min(dp[i - 1][j], dp[i][j - coins[i - 1]] + 1);                    
//                 } else {
//                     dp[i][j] = dp[i - 1][j];
//                 }
//             }
//         }
//         return dp[n][amount] == amount + 1 ? - 1 : dp[n][amount];
//     }
// };

class Solution {
public:
    int coinChange(vector<int>& coins, int amount) {
        vector<int> dp(amount + 1, amount + 1);
        dp[0] = 0;
        for (const auto& coin : coins) {
            for (int i = coin; i <= amount; i++) {
                dp[i] = min(dp[i], dp[i - coin] + 1);
            }
        }
        return dp[amount] == amount + 1 ? - 1 : dp[amount];
    }
};
```

## 416. Partition Equal Subset Sum

```cpp
// class Solution {
// public:
//     bool canPartition(vector<int>& nums) {
//         int sum = 0;
//         for (int num : nums) {
//             sum += num;
//         }
//         if (sum % 2 != 0) {
//             return false;
//         }
//         sum = sum / 2;
        
//         int n = nums.size();
//         vector<vector<bool>> dp(n + 1, vector<bool> (sum + 1));
//         for (int i = 0; i < n + 1; i++) {
//             dp[i][0] = true;
//         }
        
//         for (int i = 1; i < n + 1; i++) {
//             for (int j = 1; j < sum + 1; j++) {
//                 if (j >= nums[i - 1]) {
//                     dp[i][j] = dp[i - 1][j] || dp[i - 1][j - nums[i - 1]];
//                 } else {
//                     dp[i][j] = dp[i - 1][j];
//                 }
//             }
//         }
//         return dp[n][sum];
//     }
// };

class Solution {
public:
    bool canPartition(vector<int>& nums) {
        int sum = 0;
        for (int num : nums) {
            sum += num;
        }
        if (sum % 2 != 0) {
            return false;
        }
        sum = sum / 2;
        
        int n = nums.size();
        vector<bool> dp(sum + 1);
        dp[0] = true;
        for (int num : nums) {
            for (int j = sum; j >= num; j--) {
                dp[j] = dp[j] || dp[j - num];
            }
        }
        return dp[sum];
    }
};
```

## 494. Target Sum

```cpp
class Solution {
public:
    int findTargetSumWays(vector<int>& nums, int S) {
        int sum = 0;
        for (int num : nums) {
            sum += num;
        }
        if (S > sum || S < (-sum)) {
            return 0;
        }
        sum = sum + S;
        if (sum % 2 != 0) {
            return 0;
        }
        sum = sum / 2;
        
        vector<int> dp(sum + 1, 0);
        dp[0] = 1;
        for (int num : nums) {
            for (int j = sum; j >= num; j--) {
                dp[j] = dp[j] + dp[j - num];
            }
        }
        return dp[sum];
    }
};
```

