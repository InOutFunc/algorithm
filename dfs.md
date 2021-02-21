## 94. Binary Tree Inorder Traversal

````cpp
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    vector<int> inorderTraversal(TreeNode* root) {
        vector<int> res;
        divide(root, res);
        return res;
    }
    
private:
    void divide(TreeNode* root, vector<int>& res)
    {
        if (root == nullptr) {
            return;
        }
        divide(root->left, res);
        res.push_back(root->val);
        divide(root->right, res);
    }
};
````

##  98. Validate Binary Search Tree

```cpp
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    bool isValidBST(TreeNode* root) {
        TreeNode* pre = nullptr;
        return divide(root, pre);
    }

private:
    bool divide(TreeNode* root, TreeNode*& pre)
    {
        if (root == nullptr) {
            return true;
        }
        if (!divide(root->left, pre)) {
            return false;
        }
        if (pre != nullptr && root->val <= pre->val) {
            return false;
        }
        pre = root;
        if (!divide(root->right, pre)) {
            return false;
        }
        return true;
    }
};
```

## 101. Symmetric Tree

```cpp
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    bool isSymmetric(TreeNode* root) {
        if (root == nullptr) {
            return true;
        }
        return divide(root->left, root->right);
    }

private:
    bool divide(TreeNode* p1, TreeNode* p2)
    {
        if (p1 == nullptr && p2 == nullptr) {
            return true;
        }
        if (p1 == nullptr || p2 == nullptr) {
            return false;
        }
        if (p1->val != p2->val) {
            return false;
        }
        return divide(p1->left, p2->right) && divide(p1->right, p2->left);
    }
};
```

## 124. Binary Tree Maximum Path Sum

```cpp
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    int maxPathSum(TreeNode* root) {
        int res = INT_MIN;
        divide(root, res);
        return res;
    }
    
private:
    int divide(TreeNode* root, int& res)
    {
        if (root == nullptr) {
            return 0;
        }
        int left = max(0, divide(root->left, res));
        int right = max(0, divide(root->right, res));
        res = max(res, left + right + root->val);
        return root->val + max(left, right);
    }
};
```

##  104. Maximum Depth of Binary Tree

```cpp
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    int maxDepth(TreeNode* root) {
        if (root == nullptr) {
            return 0;
        }
        return 1 + max(maxDepth(root->left), maxDepth(root->right));
    }
};
```

## 105. Construct Binary Tree from Preorder and Inorder Traversal

```cpp
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    TreeNode* buildTree(vector<int>& preorder, vector<int>& inorder) {
        unordered_map<int, int> inorderIndex;
        for (int i = 0; i < inorder.size(); i++) {
            inorderIndex[inorder[i]] = i;
        }
        return divide(preorder, 0, preorder.size() - 1, inorder, 0, inorder.size() - 1, inorderIndex);
    }
    
private:
    TreeNode* divide(vector<int>& p, int p1, int p2, vector<int>& i, int i1, int i2, unordered_map<int, int>& inorderIndex)
    {
        if (p1 > p2) {
            return nullptr;
        }
        int left = inorderIndex[p[p1]] - i1;
        int right = i2 - inorderIndex[p[p1]];
        TreeNode* root = new TreeNode(p[p1]);
        root->left = divide(p, p1 + 1, p1 + left, i, i1, i1 + left - 1, inorderIndex);
        root->right = divide(p, p2 - right + 1, p2, i, i2 - right + 1, i2, inorderIndex);
        return root;
    }
};
```

## 114. Flatten Binary Tree to Linked List

```cpp
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    void flatten(TreeNode* root) {
        TreeNode* pre = nullptr;
        divide(root, pre);
    }
    
private:
    void divide(TreeNode* root, TreeNode*& pre)
    {
        if (root == nullptr) {
            return;
        }
        divide(root->right, pre);
        divide(root->left, pre);
        root->right = pre;
        root->left = nullptr;
        pre = root;
    }
};
```

pre既是输入，又是输出

## 200. Number of Islands

```cpp
class Solution {
public:
    int numIslands(vector<vector<char>>& grid) {
        int res = 0;
        int m = grid.size();
        int n = grid[0].size();
        vector<vector<bool>> visited(m, vector<bool>(n));
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (grid[i][j] == '1' && !visited[i][j]) {
                    res++;
                    divide(grid, visited, i, j);
                }
            }
        }
        return res;
    }
    
private:
    void divide(vector<vector<char>>& grid, vector<vector<bool>>& visited, int row, int col)
    {
        if (row < 0 || row >= grid.size() || col < 0 || col >= grid[0].size()) {
            return;
        }
        if (visited[row][col] || grid[row][col] == '0') {
            return;
        }
        visited[row][col] = true;
        divide(grid, visited, row + 1, col);
        divide(grid, visited, row - 1, col);
        divide(grid, visited, row, col + 1);
        divide(grid, visited, row, col - 1);
    }
};
```

