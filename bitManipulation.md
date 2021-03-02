## 136. Single Number

```cpp
class Solution {
public:
    int singleNumber(vector<int>& nums) {
        int res = nums[0];
        for (int i = 1; i < nums.size(); i++) {
            res = res ^ nums[i];
        }
        
        return res;
    }
};
```

## 169. Majority Element

```cpp
class Solution {
public:
    int majorityElement(vector<int>& nums) {
        int res = nums[0];
        int count = 1;
        for (int i = 1; i < nums.size(); i++) {
            if (count == 0) {
                res = nums[i];
                count = 1;
            } else if (nums[i] == res) {
                count++;
            } else {
                count--;
            }
        }
        
        return res;
    }
};
```

## 338. Counting Bits

```cpp
class Solution {
public:
    vector<int> countBits(int num) {
        vector<int> dp(num + 1);
        for (int i = 1; i < num + 1; i++) {
            dp[i] = dp[i & (i - 1)] + 1;
        }
        return dp;
    }
};
```

