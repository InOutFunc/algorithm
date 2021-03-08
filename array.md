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

## jz19 顺时针的顺序依次打印出每一个数字

```cpp
class Solution {
public:
    vector<int> printMatrix(vector<vector<int> > matrix) {
        int startRow = 0;
        int endRow = matrix.size() - 1;
        int startCol = 0;
        int endCol = matrix[0].size() - 1;
        int dir = 0;
        vector<int> res;
        while (startRow <= endRow && startCol <= endCol) {
            switch (dir) {
                case 0:
                    for (int col = startCol; col <= endCol; col++) {
                        res.push_back(matrix[startRow][col]);
                    }
                    startRow++;
                    break;
                case 1:
                    for (int row = startRow; row <= endRow; row++) {
                        res.push_back(matrix[row][endCol]);
                    }
                    endCol--;
                    break;
                case 2:
                    for (int col = endCol; col >= startCol; col--) {
                        res.push_back(matrix[endRow][col]);
                    }
                    endRow--;
                    break;
                case 3:
                    for (int row = endRow; row >= startRow; row--) {
                        res.push_back(matrix[row][startCol]);
                    }
                    startCol++;
                    break;
            }
            dir = (dir + 1) % 4;
        }
        
        return res;
    }
};
```

