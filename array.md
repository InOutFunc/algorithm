## 48. Rotate Image

```cpp
class Solution {
public:
    void rotate(vector<vector<int>>& matrix) {
        for (int i = 0; i < matrix.size() / 2; i++) {
            swap(matrix[i], matrix[matrix.size() - i - 1]);
        }
        
        for (int i = 0; i < matrix.size() - 1; i++) {
            for (int j = i + 1; j < matrix.size(); j++) {
                swap(matrix[i][j], matrix[j][i]);
            }
        }
    }
};
```

