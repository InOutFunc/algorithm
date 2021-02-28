## 207. Course Schedule

```cpp
class Solution {
public:
    bool canFinish(int numCourses, vector<vector<int>>& prerequisites) {
        map<int, vector<int>> oneToAll;
        vector<int> indegree(numCourses);
        for (const auto& item : prerequisites) {
            oneToAll[item[1]].push_back(item[0]);
            indegree[item[0]]++;
        }
        queue<int> q;
        for (int i = 0; i < numCourses; i++) {
            if (indegree[i] == 0) {
                q.push(i);
            }
        }
        while (!q.empty()) {
            int cur = q.front();
            q.pop();
            numCourses--;
            for (const auto& item : oneToAll[cur]) {
                if (--indegree[item] == 0) {
                    q.push(item);
                }
            }
        }
        return numCourses == 0;
    }
};
```

