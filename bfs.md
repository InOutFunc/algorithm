## 45. Jump Game II

```cpp
class Solution {
public:
    int jump(vector<int>& nums) {
        int nextLevelEnd = 0;
        int res = 0;
        int curlevelEnd = 0;
        for (int i = 0; i < nums.size() - 1; i++) {
            nextLevelEnd = max(nextLevelEnd, i + nums[i]);
            if (i == curlevelEnd) {
                res++;
                curlevelEnd = nextLevelEnd;
            }
        }
        
        return res;
    }
};
```

## 55. Jump Game

```cpp
class Solution {
public:
    bool canJump(vector<int>& nums) {
        int curLevelEnd = 0;
        int nextLevelEnd = 0;
        for (int i = 0; i < nums.size() - 1; i++) {
            nextLevelEnd = max(nextLevelEnd, i + nums[i]);
            if (i == curLevelEnd) {
                if (curLevelEnd == nextLevelEnd) {
                    return false;
                }
                curLevelEnd = nextLevelEnd;
            }
        }
        return true;
    }
};
```

