```
```
```cpp
// cpp : preOrder + 递归
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
    vector<vector<int>> pathSum(TreeNode* root, int sum) {
        std::vector<int> path;
        std::vector<vector<int>> res;
        pathSum(root, sum, path, res);
        return res;
    }
    
    void pathSum(TreeNode* root, int sum, std::vector<int>& path, std::vector<vector<int>>& res) {
        if( root == nullptr){
            return ;
        }
            
        path.emplace_back(root->val);
        if(root->left == nullptr && root->right == nullptr && root->val == sum){
            res.emplace_back(path);
        }
        
        pathSum(root->left, sum - root->val, path, res);
        pathSum(root->right, sum - root->val, path, res);
        
        path.pop_back();
    }
};
```
```cpp
// cpp: preOrder + 递归 + labda
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
    vector<vector<int>> pathSum(TreeNode* root, int sum) {
        std::vector<int> path;
        std::vector<vector<int>> res;
        std::function<void(TreeNode*, int)> pathSumProxy = [&](TreeNode* root, int sum){
            if( root == nullptr){
                return ;
            }
            
            path.emplace_back(root->val);
            if(root->left == nullptr && root->right == nullptr && root->val == sum){
                res.emplace_back(path);
            }

            pathSumProxy(root->left, sum - root->val);
            pathSumProxy(root->right, sum - root->val);

            path.pop_back();
        };
        pathSumProxy(root, sum);
        return res;
    }
};
```
