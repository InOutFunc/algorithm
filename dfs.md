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

## 226. Invert Binary Tree

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
    TreeNode* invertTree(TreeNode* root) {
        if (root == nullptr) {
            return nullptr;
        }
        TreeNode* tmp = root->left;
        root->left = invertTree(root->right);
        root->right = invertTree(tmp);
        return root;
    }
};
```

## 230. Kth Smallest Element in a BST

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
    int kthSmallest(TreeNode* root, int k) {
        int res = 0;
        divide(root, k, res);
        return res;
    }
private:
    void divide(TreeNode* root, int& k, int& res)
    {
        if (root == nullptr) {
            return;
        }
        if (k < 1) {
            return;
        }
        divide(root->left, k, res);
        if (k-- == 1) {
            res = root->val;
            return;
        }
        divide(root->right, k, res);
    }
};
```

## 236. Lowest Common Ancestor of a Binary Tree

```cpp
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
        if (root == nullptr) {
            return nullptr;
        }
        if (root == p || root == q) {
            return root;
        }
        TreeNode* left = lowestCommonAncestor(root->left, p, q);
        TreeNode* right = lowestCommonAncestor(root->right, p, q);
        if (left != nullptr && right != nullptr) {
            return root;
        }
        if (left == nullptr) {
            return right;
        }
        return left;
    }
};
```

## 297. Serialize and Deserialize Binary Tree

```cpp
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Codec {
public:

    // Encodes a tree to a single string.
    string serialize(TreeNode* root) {
        ostringstream oss;
        seDivide(root, oss);
        return oss.str();
    }

    // Decodes your encoded data to tree.
    TreeNode* deserialize(string data) {
        istringstream iss(data);
        return deDivide(iss);
    }
private:
    void seDivide(TreeNode* root, ostringstream& oss)
    {
        if (root == nullptr) {
            oss << '#' << ' ';
            return;
        }
        oss << root->val << ' ';
        seDivide(root->left, oss);
        seDivide(root->right, oss);
    }
    TreeNode* deDivide(istringstream& iss)
    {
        string tmp;
        iss >> tmp;
        if (tmp == "#") {
            return nullptr;
        }
        TreeNode* root = new TreeNode(stoi(tmp));
        root->left = deDivide(iss);
        root->right = deDivide(iss);
        return root;
    }
};

// Your Codec object will be instantiated and called as such:
// Codec ser, deser;
// TreeNode* ans = deser.deserialize(ser.serialize(root));
```

## 337. House Robber III

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
    int rob(TreeNode* root) {
        vector<int> res = divide(root);
        return max(res[0], res[1]);
    }
private:
    vector<int> divide(TreeNode* root)
    {
        if (root == nullptr) {
            return {0, 0};
        }
        vector<int> left = divide(root->left);
        vector<int> right = divide(root->right);
        vector<int> res(2);
        res[0] = max(left[0], left[1]) + max(right[0], right[1]);
        res[1] = left[0] + right[0] + root->val;
        return res;
    }
};
```

## 543. Diameter of Binary Tree

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
    int diameterOfBinaryTree(TreeNode* root) {
        int res = 0;
        divide(root, res);
        return res;
    }
private:
    int divide(TreeNode* root, int& res)
    {
        if (root == nullptr) {
            return 0;
        }
        int left = divide(root->left, res);
        int right = divide(root->right, res);
        res = max(res, left + right);
        return max(left, right) + 1;
    }
};
```

## 617. Merge Two Binary Trees

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
    TreeNode* mergeTrees(TreeNode* root1, TreeNode* root2) {
        if (root1 == nullptr) {
            return root2;
        }
        if (root2 == nullptr) {
            return root1;
        }
        TreeNode* root = new TreeNode(root1->val + root2->val);
        root->left = mergeTrees(root1->left, root2->left);
        root->right = mergeTrees(root1->right, root2->right);
        return root;
    }
};
```

## jz17 判断B是不是A的子结构

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
    bool HasSubtree(TreeNode* pRoot1, TreeNode* pRoot2)
    {
        if (pRoot2 == nullptr || pRoot1 == nullptr) {
            return false;
        }
        if (IsSubtree(pRoot1, pRoot2)) {
            return true;
        }
        return IsSubtree(pRoot1->left, pRoot2) || IsSubtree(pRoot1->right, pRoot2);
    }
    
private:
    bool IsSubtree(TreeNode* p1, TreeNode* p2)
    {
        if (p2 == nullptr) {
            return true;
        }
        if (p1 == nullptr) {
            return false;
        }
        return (p1->val == p2->val) && IsSubtree(p1->left, p2->left) && IsSubtree(p1->right, p2->right);
    }
};
```

## jz23 二叉搜索树的后序遍历的结果

```cpp
class Solution {
public:
    bool VerifySquenceOfBST(vector<int> sequence) {
        if (sequence.empty()) {
            return false;
        }
        return divide(sequence, 0, sequence.size() - 1);
    }

private:
    bool divide(const vector<int>& s, int l, int r)
    {
        if (l >= r) {
            return true;
        }
        int val = s[r];
        int i = l;
        while (i < r) {
            if (s[i] >val) {
                break;
            }
            i++;
        }
        for (int j = i; j < r; j++) {
            if (s[j] < val) {
                return false;
            }
        }
        return divide(s, l, i - 1) && divide(s, i, r - 1);
    }
};
```

## jz26 将该二叉搜索树转换成一个排序的双向链表

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
    TreeNode* Convert(TreeNode* root)
    {
        if (!root) return NULL;
        TreeNode *head = NULL, *pre = NULL;
        inorder(root, pre, head);
//         pre->right = head;
//         head->left = pre;
        return head;
    }
    
private:
    void inorder(TreeNode* node, TreeNode*& pre, TreeNode*& head) {
        if (!node) return;
        inorder(node->left, pre, head);
        if (!head) {
            head = node;
            pre = node;
        } else {
            pre->right = node;
            node->left = pre;
            pre = node;
        }
        inorder(node->right, pre, head);
    }
};
```

## jz39 判断该二叉树是否是平衡二叉树

```cpp
class Solution {
public:
    bool IsBalanced_Solution(TreeNode* pRoot) {
        if (divide(pRoot) == -1) {
            return false;
        }
        return true;
    }
private:
    int divide(TreeNode* pRoot)
    {
        if (pRoot == nullptr) {
            return 0;
        }
        int left = divide(pRoot->left);
        if (left == -1) {
            return -1;
        }
        int right = divide(pRoot->right);
        if (right == -1) {
            return -1;
        }
        if (abs(left - right) > 1) {
            return -1;
        }
        return max(left, right) + 1;
    }
};
```

