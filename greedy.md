## 406. Queue Reconstruction by Height

```cpp
class Solution {
public:
    vector<vector<int>> reconstructQueue(vector<vector<int>>& people) {
        sort(people.begin(), people.end(), [] (const auto& a, const auto& b) {
            return a[0] > b[0] || (a[0] == b[0] && a[1] < b[1]);
        });
    
        vector<vector<int>> res;
        for (int i = 0; i < people.size(); i++) {
            res.insert(res.begin() + people[i][1], people[i]);
        }

        return res;
    }
};
```

## 621. Task Scheduler

```cpp
class Solution {
public:
    int leastInterval(vector<char>& tasks, int n) {
        unordered_map<char, int> taskCnt;
        int maxSize = 0;
        for (char ch : tasks) {
            taskCnt[ch]++;
            maxSize = max(maxSize, taskCnt[ch]);
        }
        
        int res = (maxSize - 1) * (n + 1);
        for (auto& kv : taskCnt) {
            if (kv.second == maxSize) {
                res++;
            }
        }
        
        if (res < tasks.size()) {
            return tasks.size();
        }
        return res;
    }
};
```

## 763. Partition Labels

```cpp
class Solution {
public:
    vector<int> partitionLabels(string S) {
        unordered_map<char, int> lastPos;
        for (int i = 0; i < S.size(); i++) {
            lastPos[S[i]] = i;
        }
        vector<int> res;
        int l = 0;
        int r = 0;
        int maxPos = -1;
        while (r < S.size()) {
            maxPos = max(maxPos, lastPos[S[r]]);
            if (r == maxPos) {
                res.push_back(r - l + 1);
                l = r + 1;
            }
            r++;
        }
        return res;
    }
};
```

