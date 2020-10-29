```
Given a binary tree, return the level order traversal of its nodes' values. (ie, from left to right, level by level).

For example:
Given binary tree [3,9,20,null,null,15,7],

    3
   / \
  9  20
    /  \
   15   7

return its level order traversal as:

[
  [3],
  [9,20],
  [15,7]
]
```
```cpp
// BFS
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
        if(root == nullptr){
            return {};
        }
        
        std::vector<std::vector<int>> result;
        std::queue<TreeNode*> q;
        q.emplace(root);
        // visited = set(root); // for 图
        while(!q.empty()){
            int size = q.size();
            vector<int> vec;
            for(int i = 0; i < size; i++){
                auto node = q.front();
                q.pop();
                vec.emplace_back(node->val);
                if(node->left != nullptr){
                    q.emplace(node->left);
                }
                if(node->right != nullptr){
                    q.emplace(node->right);
                }
            }
            result.emplace_back(vec);
        }
        
        return result;
    }
};
```

```cpp
// DFS + 递归
class Solution {
public:
    vector<vector<int>> levelOrder(TreeNode* root) {
        if(root == nullptr){
            return {};
        }
        
        std::vector<std::vector<int>> result;
        dfs(root, result, 0);
        
        return result;
    }
    
    void dfs(TreeNode* root, std::vector<std::vector<int>>& result, int level){
        if( root == nullptr ){
            return ;
        }
        
        if(result.size() < level + 1){
            result.emplace_back(std::vector<int>{root->val});
        }else{
            result[level].emplace_back(root->val);
        }
        
        dfs(root->left, result, level+1);
        dfs(root->right, result, level+1);
    }
};
```
