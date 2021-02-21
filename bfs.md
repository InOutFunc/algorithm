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

##  102. Binary Tree Level Order Traversal

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
    vector<vector<int>> levelOrder(TreeNode* root) {
        if (root == nullptr) {
            return {};
        }
        queue<TreeNode*> q;
        q.push(root);
        vector<vector<int>> res;
        while (!q.empty()) {
            int n = q.size();
            vector<int> level(n);
            for (int i = 0; i < n; i++) {
                TreeNode* tmp = q.front();
                q.pop();
                level[i] = tmp->val;
                if (tmp->left != nullptr) {
                    q.push(tmp->left);
                }
                if (tmp->right != nullptr) {
                    q.push(tmp->right);
                }
            }
            res.push_back(level);
        }
        
        return res;
    }
};
```

## 199. Binary Tree Right Side View

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
    vector<int> rightSideView(TreeNode* root) {
        if (root == nullptr) {
            return {};
        }
        vector<int> res;
        queue<TreeNode*> q;
        q.push(root);
        while (!q.empty()) {
            int n = q.size();
            vector<int> level(n);
            for (int i = 0; i < n; i++) {
                TreeNode* tmp = q.front();
                q.pop();
                level[i] = tmp->val;
                if (tmp->left != nullptr) {
                    q.push(tmp->left);
                }
                if (tmp->right != nullptr) {
                    q.push(tmp->right);
                }
            }
            res.push_back(level[n - 1]);
        }
        return res;
    }
};
```

