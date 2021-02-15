## 56. Merge Intervals

```cpp
class Solution {
public:
    vector<vector<int>> merge(vector<vector<int>>& intervals) {
        sort(intervals.begin(), intervals.end(), [] (const auto&item1, const auto& item2) {
            return item1[0] < item2[0];
        });
        
        vector<vector<int>> res;
        res.push_back(intervals[0]);
        for (int i = 1; i < intervals.size(); i++) {
            if (intervals[i][0] > res.back()[1]) {
                res.push_back(intervals[i]);
                continue;
            }
            if (res.back()[1] > intervals[i][1]) {
                continue;
            }
            res.back()[1] = intervals[i][1];
        }
        
        return res;
    }
};
```

