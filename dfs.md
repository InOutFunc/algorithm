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

