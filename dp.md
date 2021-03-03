## 5. Longest Palindromic Substring

```cpp
class Solution {
public:
    string longestPalindrome(string s) {
        int size = s.size();
        vector<vector<bool>> dp(size, vector<bool>(size, false));
        for (int i = 0; i < size; i++) {
            dp[i][i] = true;
        }
        for (int i = 0; i < size - 1; i++) {
            dp[i][i + 1] = (s[i] == s[i + 1]);
        }
        for (int k = 2; k < size; k++) {
            for (int i = 0; i < size - k; i++) {
                dp[i][i + k] = (s[i] == s[i + k]) && dp[i + 1][i + k -1];
            }
        }
        int max = 0;
        int start = 0;
        int end = 0;
        for (int i = 0; i < size; i++) {
            for (int j = i; j < size; j++) {
                if (dp[i][j] && (j - i + 1) > max) {
                    max = j - i + 1;
                    start = i;
                    end = j;
                }
            }
        }
        return s.substr(start, end - start + 1);
    }
};
```

## 10. Regular Expression Matching

```cpp
class Solution {
public:
    bool isMatch(string s, string p) {
        int m = s.size();
        int n = p.size();
        vector<vector<bool>> dp(m + 1, vector<bool>(n + 1));
        dp[0][0] = true;
        
        for (int j = 2; j < n + 1; j++) {
            dp[0][j] = (p[j - 1] == '*' && dp[0][j - 2]);
        }
        
        for (int i = 1; i < m + 1; i++) {
            for (int j = 1; j < n + 1; j++) {
                if (p[j - 1] == s[i - 1] || p[j - 1] == '.') {
                    dp[i][j] = dp[i - 1][j - 1];
                } else if (p[j - 1] == '*') {
                    if (p[j - 2] == s[i - 1] || p[j - 2] == '.') {
                        dp[i][j] = dp[i][j - 2] || dp[i - 1][j - 1] || dp[i - 1][j];
                    } else {
                        dp[i][j] = dp[i][j - 2];
                    }
                }
            }
        }
        
        return dp[m][n];
    }
};
```

## 53. Maximum Subarray

```cpp
class Solution {
public:
    int maxSubArray(vector<int>& nums) {
        int n = nums.size();
        vector<int> dp(n);
        dp[0] = nums[0];
        for (int i = 1; i < n; i++) {
            if (dp[i - 1] > 0) {
                dp[i] = dp[i - 1] + nums[i];
            } else {
                dp[i] = nums[i];
            }
        }
        
        return *max_element(dp.begin(), dp.end());
    }
};
```

## 62. Unique Paths

```cpp
class Solution {
public:
    int uniquePaths(int m, int n) {
        vector<vector<int>> dp(m, vector<int>(n, 1));
        for (int i = 1; i < m; i++) {
            for (int j = 1; j < n; j++) {
                dp[i][j] = dp[i][j - 1] + dp[i - 1][j];
            }
        }
        return dp[m - 1][n - 1];
    }
};
```

## 64. Minimum Path Sum

```cpp
class Solution {
public:
    int minPathSum(vector<vector<int>>& grid) {
        int m = grid.size();
        int n = grid[0].size();
        vector<vector<int>> dp(m, vector<int>(n));
        dp[0][0] = grid[0][0];
        for (int i = 1; i < m; i++) {
            dp[i][0] = dp[i - 1][0] + grid[i][0];
        }
        for (int j = 1; j < n; j++) {
            dp[0][j] = dp[0][j - 1] + grid[0][j];
        }
        for (int i = 1; i < m; i++) {
            for (int j = 1; j < n; j++) {
                dp[i][j] = min(dp[i - 1][j], dp[i][j - 1]) + grid[i][j];
            }
        }
        
        return dp[m - 1][n - 1];
    }
};
```

##  70. Climbing Stairs

```cpp
class Solution {
public:
    int climbStairs(int n) {
        if (n < 3) {
            return n;
        }
        vector<int> dp(n + 1);
        dp[1] = 1;
        dp[2] = 2;
        for (int i = 3; i <= n; i++) {
            dp[i] = dp[i - 1] + dp[i - 2];
        }
        return dp[n];
    }
};
```

## 72. Edit Distance

```cpp
class Solution {
public:
    int minDistance(string word1, string word2) {
        int m = word1.size();
        int n = word2.size();
        vector<vector<int>> dp(m + 1, vector<int>(n + 1));
        for (int i = 1; i < m + 1; i++) {
            dp[i][0] = dp[i - 1][0] + 1;
        }
        for (int j = 1; j < n + 1; j++) {
            dp[0][j] = dp[0][j - 1] + 1;
        }
        
        for (int i = 1; i < m + 1; i++) {
            for (int j = 1; j < n + 1; j++) {
                if (word1[i - 1] == word2[j - 1]) {
                    dp[i][j] = dp[i - 1][j - 1];
                } else {
                    dp[i][j] = min(min(dp[i][j - 1], dp[i - 1][j]), dp[i - 1][j - 1]) + 1;
                }
            }
        }
        
        return dp[m][n];
    }
};
```

## 84. Largest Rectangle in Histogram

```cpp
class Solution {
public:
    int largestRectangleArea(vector<int>& heights) {
        int n = heights.size();
        vector<int> lessFromLeft(n);
        vector<int> lessFromRight(n);
        
        lessFromLeft[0] = -1;
        for (int i = 1; i < n; i++) {
            int j = i - 1;
            while (j >= 0 && heights[j] >= heights[i]) {
                j = lessFromLeft[j];
            }
            lessFromLeft[i] = j;
        }
        
        lessFromRight[n - 1] = n;
        for (int i = n - 2; i >= 0; i--) {
            int j = i + 1;
            while (j < n && heights[j] >= heights[i]) {
                j = lessFromRight[j];
            }
            lessFromRight[i] = j;
        }
        
        int res = 0;
        for (int i = 0; i < n; i++) {
            res = max(res, (lessFromRight[i] - lessFromLeft[i] - 1) * heights[i]);
        }
        
        return res;
    }
};
```

## 85. Maximal Rectangle

````cpp
class Solution {
public:
    int maximalRectangle(vector<vector<char>>& matrix) {
        if (matrix.empty() || matrix[0].empty()) {
            return 0;
        }
        int m = matrix.size();
        int n = matrix[0].size();
        vector<int> h(n);
        vector<int> l(n);
        vector<int> r(n, n - 1);
        int res = 0;
        
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (matrix[i][j] == '0') {
                    h[j] = 0;
                } else {
                    h[j] = h[j] + 1;
                }
            }
            
            int curLeft = 0;
            for (int j = 0; j < n; j++) {
                if (matrix[i][j] == '0') {
                    curLeft = j + 1;
                    l[j] = 0;
                } else {
                    l[j] = max(curLeft, l[j]);
                }
            }
            
            int curRight = n - 1;
            for (int j = n - 1; j >= 0; j--) {
                if (matrix[i][j] == '0') {
                    curRight = j - 1;
                    r[j] = n - 1;
                } else {
                    r[j] = min(curRight, r[j]);
                }
            }
            
            for (int i = 0; i < n; i++) {
                res = max(res, h[i] * (r[i] - l[i] + 1));
            }
        }
        
        return res;
    }
};
````

##  96. Unique Binary Search Trees

````cpp
class Solution {
public:
    int numTrees(int n) {
        vector<int> dp(n + 1);
        dp[0] = 1;
        for (int i = 1; i < n + 1; i++) {
            for (int k = 0; k < i; k++) {
                dp[i] += dp[k] * dp[i - 1 - k];
            }
        }
        
        return dp[n];
    }
};
````

## 139. Word Break

```cpp
class Solution {
public:
    bool wordBreak(string s, vector<string>& wordDict) {
        unordered_set<string> wordSet(wordDict.begin(), wordDict.end());
        vector<bool> dp(s.size() + 1);
        dp[0] = true;
        
        for (int i = 1; i < dp.size(); i++) {
            for (int j = 0; j < i; j++) {
                dp[i] = (wordSet.find(s.substr(j, i - j)) != wordSet.end() && dp[j]);
                if (dp[i]) {
                    break;
                }
            }
        }
        
        return dp.back();
    }
};
```

## 152. Maximum Product Subarray

```cpp
class Solution {
public:
    int maxProduct(vector<int>& nums) {
        int res = nums[0];
        int curMax = nums[0];
        int curMin = nums[0];
        for (int i = 1; i < nums.size(); i++) {
            if (nums[i] < 0) {
                swap(curMax, curMin);
            }
            curMax = max(nums[i], curMax * nums[i]);
            curMin = min(nums[i], curMin * nums[i]);
            res = max(res, curMax);
        }
        return res;
    }
};
```

## 198 House Robber

```cpp
class Solution {
public:
    int rob(vector<int>& nums) {
        if (nums.empty()) {
            return 0;
        }
        vector<int> dp(nums.size());
        dp[0] = nums[0];
        if (nums.size() == 1) {
            return dp[0];
        }
        dp[1] = nums[1];
        if (nums.size() == 2) {
            return max(dp[0], dp[1]);
        }
        dp[2] = max(dp[1], dp[0] + nums[2]);
        for (int i = 3; i < nums.size(); i++) {
            dp[i] = max(dp[i - 2], dp[i - 3]) + nums[i];
        }
        return *max_element(dp.begin(), dp.end());
    }
};
```

## 221. Maximal Square

```cpp
class Solution {
public:
    int maximalSquare(vector<vector<char>>& matrix) {
        int m = matrix.size();
        int n = matrix[0].size();
        vector<vector<int>> dp(m + 1, vector<int>(n + 1));
        int res = 0;
        for (int i = 1; i < m + 1; i++) {
            for (int j = 1; j < n + 1; j++) {
                if (matrix[i - 1][j - 1] != '0') {
                    dp[i][j] = min(dp[i - 1][j - 1], min(dp[i][j - 1], dp[i - 1][j])) + 1;
                    res = max(res, dp[i][j] * dp[i][j]);
                }
            }
        }
        return res;
    }
};
```

## 238. Product of Array Except Self

```cpp
class Solution {
public:
    vector<int> productExceptSelf(vector<int>& nums) {
        vector<int> res(nums.size());
        res[0] = 1;
        for (int i = 1; i < nums.size(); i++) {
            res[i] = res[i - 1] * nums[i - 1];
        }
        for (int right = 1, j = nums.size() - 1; j >= 0; j--) {
            res[j] = res[j] * right;
            right *= nums[j];
        }
        return res;
    }
};
```

## 279. Perfect Squares

```cpp
class Solution {
public:
    int numSquares(int n) {
        vector<int> dp(n + 1, INT_MAX);
        dp[0] = 0;
        for (int i = 1; i < n + 1; i++) {
            for (int j = 1; j * j <= i; j++) {
                dp[i] = min(dp[i], dp[i - j * j] + 1);
            }
        }
        return dp[n];
    }
};
```

## 309. Best Time to Buy and Sell Stock with Cooldown

```cpp
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        if (prices.empty()) {
            return 0;
        }
        int n = prices.size();
        vector<int> idle(n);
        vector<int> hold(n);
        vector<int> justSold(n);
        idle[0] = 0;
        hold[0] = -prices[0];
        justSold[0] = 0;
        for (int i = 1; i < n; i++) {
            idle[i] = max(idle[i - 1], justSold[i - 1]);
            hold[i] = max(hold[i - 1], idle[i - 1] - prices[i]);
            justSold[i] = hold[i - 1] + prices[i];
        }
        return max(idle[n - 1], justSold[n - 1]);
    }
};
```

## 647. Palindromic Substrings

```cpp
class Solution {
public:
    int countSubstrings(string s) {
        int n = s.size();
        vector<vector<bool>> dp(n, vector<bool>(n));
        for (int i = 0; i < n; i++) {
            dp[i][i] = true;
        }
        for (int i = 0; i < n - 1; i++) {
            dp[i][i + 1] = (s[i] == s[i + 1]);
        }
        for (int k = 3; k <= n; k++) {
            for (int i = 0; i <= n - k; i++) {
                dp[i][i + k - 1] = dp[i + 1][i + k - 2] && (s[i] == s[i + k - 1]);
            }
        }
        
        int res = 0;
        for (int i = 0; i < n; i++) {
            for (int j = i; j < n ;j++) {
                if (dp[i][j]) {
                    res++;
                }
            }
        }
        return res;
    }
};
```
