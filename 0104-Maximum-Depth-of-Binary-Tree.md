```
Given a binary tree, find its maximum depth.

The maximum depth is the number of nodes along the longest path from the root node down to the farthest leaf node.

Note: A leaf is a node with no children.

Example:

Given binary tree [3,9,20,null,null,15,7],

    3
   / \
  9  20
    /  \
   15   7

return its depth = 3.
```
```
method: 
1: 递归
2.1: DFS + 递归： 记录根节点到每个叶子结点的深度，同时保存最大值
2.2: DFS + 栈：
3: BFS： 层数就是最大值
```
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
    
        return 1 + std::max(maxDepth(root->left), maxDepth(root->right));
    }
};
```
```cpp
// DFS + 递归
class Solution {
public:
    int maxDepth(TreeNode* root) {
        if (root == nullptr) {
            return 0;
        }
        int maxVal = 0;
        dfs(root, maxVal, 0);
        return maxVal;
    }
    
    void dfs(TreeNode* root, int& maxVal, int level){
        if ( root == nullptr ) {
            return ;
        }
        
        if ( root->left == nullptr && root->right == nullptr ){
            maxVal = std::max(maxVal, level+1);
            return ;
        }
        
        if ( root->left != nullptr ){
            dfs(root->left, maxVal, level+1);
        }
        if ( root->right != nullptr ){
            dfs(root->right, maxVal, level+1);
        }
    }
};
```
```cpp
// DFS + Stack
class Solution {
public:
    int maxDepth(TreeNode* root) {
        if ( root == nullptr ) {
            return 0;
        }
        
        if ( root->left == nullptr && root->right == nullptr ){
            return 1;
        }
        
        int result = 0;
        std::stack<std::pair<TreeNode*, int>> s;
        s.emplace(std::make_pair(root, 1));
        while (!s.empty()) {
            auto node = s.top();
            s.pop();
            if ( node.first->left == nullptr && node.first->right == nullptr ){ //对于求max的情况可以不加判断
                result = std::max(result, node.second);
            }
            if ( node.first->left != nullptr ) {
                s.emplace(std::make_pair(node.first->left, node.second+1));
            }
            if ( node.first->right != nullptr ) {
                s.emplace(std::make_pair(node.first->right, node.second+1));
            }
        }
        
        return result;
    }
};
```
