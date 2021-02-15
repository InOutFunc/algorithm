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