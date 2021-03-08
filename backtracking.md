## 17. Letter Combinations of a Phone Number

```cpp
class Solution {
public:
    vector<string> letterCombinations(string digits) {
        if (digits.empty()) {
            return {};
        }
        string cur;
        vector<string> res;
        map<char, string> table = {
            {'2', "abc"},{'3', "def"},{'4', "ghi"},
            {'5', "jkl"},{'6', "mno"},{'7', "pqrs"},
            {'8', "tuv"},{'9', "wxyz"},
        };
        divide(digits, cur, res, table);
        return res;
    }
    
private:
    void divide(string digits, string& cur, vector<string>& res, map<char, string>& table)
    {
        if (cur.size() == digits.size()) {
            res.push_back(cur);
        }
        int n = cur.size();
        for (int i = 0; i < table[digits[n]].size(); i++) {
            cur.push_back(table[digits[n]][i]);
            divide(digits, cur, res, table);
            cur.pop_back();
        }
    }
};
```

## 22. Generate Parentheses

```cpp
class Solution {
public:
    vector<string> generateParenthesis(int n) {
        vector<string> res;
        string cur;
        divide(n, 0, cur, res);
        return res;
    }
    
private:
    void divide(int n, int left, string& cur, vector<string>& res)
    {
        if (cur.size() == n * 2) {
            res.push_back(cur);
            return;
        }
        if (left < n) {
            cur.push_back('(');
            divide(n, left + 1, cur, res);
            cur.pop_back();
        }
        if (left > cur.size() - left) {
            cur.push_back(')');
            divide(n, left, cur, res);
            cur.pop_back();
        }
    }
};
```

## 39. Combination Sum

```cpp
class Solution {
public:
    vector<vector<int>> combinationSum(vector<int>& candidates, int target) {
        vector<int> cur;
        vector<vector<int>> res;
        divide(candidates, 0, target, cur, res);
        return res;
    }
    
private:
    void divide(vector<int>& nums, int start, int target, vector<int>& cur, vector<vector<int>>& res)
    {
        if (target < 0) {
            return;
        }
        if (target == 0) {
            res.push_back(cur);
        }
        for (int i = start; i < nums.size(); i++) {
            cur.push_back(nums[i]);
            divide(nums, i, target - nums[i], cur, res);
            cur.pop_back();
        }
    }
};
// 每个divide是同一层中的不同分支，假设最后一层有三个结果，就有到下面一层再返回
```

## 46. Permutations

```cpp
class Solution {
public:
    vector<vector<int>> permute(vector<int>& nums) {
        vector<int> cur;
        vector<int> used(nums.size());
        vector<vector<int>> res;
        divide(nums, cur, used, res);
        return res;
    }
    
private:
    void divide(vector<int>& nums, vector<int>& cur, vector<int>& used, vector<vector<int>>& res)
    {
        if (cur.size() == nums.size()) {
            res.push_back(cur);
            return;
        }
        for (int i = 0; i < nums.size(); i++) {
            if (used[i] == 1) {
                continue;
            }
            used[i] = 1;
            cur.push_back(nums[i]);
            divide(nums, cur, used, res);
            cur.pop_back();
            used[i] = 0;
        }
    }
};
```

## 78. Subsets

```cpp
class Solution {
public:
    vector<vector<int>> subsets(vector<int>& nums) {
        vector<int> cur;
        vector<vector<int>> res;
        divide(nums, 0, cur, res);
        return res;
    }
    
private:
    void divide(vector<int>& nums, int start, vector<int>& cur, vector<vector<int>>& res)
    {
        res.push_back(cur);
        if (start == nums.size()) {
            return;
        }
        for (int i = start; i < nums.size(); i++) {
            cur.push_back(nums[i]);
            divide(nums, i + 1, cur, res);
            cur.pop_back();
        }
    }
};
```

## 79. Word Search

```cpp
class Solution {
public:
    bool exist(vector<vector<char>>& board, string word) {
        string cur;
        int rows = board.size();
        int cols = board[0].size();
        vector<vector<bool>> visited(rows, vector<bool>(cols));
        for (int i = 0; i < rows; i++) {
            for (int j = 0; j < cols; j++) {
                if (divide(board, word, i, j, cur, visited)) {
                    return true;
                }
            }
        }
        return false;
    }
    
private:
    bool divide(vector<vector<char>>& board, string word, int row, int col, string& cur, vector<vector<bool>>& visited)
    {
        int n = cur.size();
        if (n == word.size()) {
            return true;
        }
        if (row < 0 || row >= board.size() || col < 0 || col >= board[0].size()) {
            return false;
        }
        if (visited[row][col] || board[row][col] != word[n]) {
            return false;
        }
        visited[row][col] = true;
        cur.push_back(board[row][col]);
        bool res =  divide(board, word, row + 1, col, cur, visited) ||
            divide(board, word, row - 1, col, cur, visited) ||
            divide(board, word, row, col + 1, cur, visited) ||
            divide(board, word, row, col - 1, cur, visited);
        cur.pop_back();
        visited[row][col] = false;
        return res;
    }
};
```

## jz24 二叉树中结点值的和为输入整数的所有路径

```cpp
/*
struct TreeNode {
	int val;
	struct TreeNode *left;
	struct TreeNode *right;
	TreeNode(int x) :
			val(x), left(NULL), right(NULL) {
	}
};*/
class Solution {
public:
    vector<vector<int> > FindPath(TreeNode* root,int expectNumber) {
        vector<vector<int>> res;
        divide(root, expectNumber, {}, res);
        return res;
    }
    
private:
    void divide(TreeNode* root, int n, vector<int> cur, vector<vector<int>>& res)
    {
        if (root == nullptr) {
            return;
        }
        if (n < 0) {
            return;
        }
        int val = root->val;
        if (val == n && root->left == nullptr && root->right == nullptr) {
            cur.push_back(val);
            res.push_back(cur);
            return;
        }
        cur.push_back(val);
        divide(root->left, n - val, cur, res);
        divide(root->right, n - val, cur, res);
    }
};
```

## jz27 按字典序打印出该字符串中字符的所有排列

```cpp
class Solution {
public:
    vector<string> Permutation(string str) {
        sort(str.begin(), str.end());
        string cur;
        vector<bool> visited(str.size());
        vector<string> res;
        divide(str, cur, res, visited);
        return res;
    }
    
private:
    void divide(string str, string& cur, vector<string>& res, vector<bool>& visited)
    {
        if (cur.size() == str.size()) {
            res.push_back(cur);
            return;
        }
        for (int i = 0; i < str.size(); i++) {
            if (visited[i]) {
                continue;
            }
            if (i > 0 && str[i] == str[i - 1] && !visited[i - 1]) {
                continue;
            }
            cur.push_back(str[i]);
            visited[i] = true;
            divide(str, cur, res, visited);
            visited[i] = false;
            cur.pop_back();
        }
        
    }
};


/*
abc



*/
```

