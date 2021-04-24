```
Given the root of a binary tree, return the zigzag level order traversal of its nodes' values. (i.e., from left to right, then right to left for the next level and alternate between).

 

Example 1:


Input: root = [3,9,20,null,null,15,7]
Output: [[3],[20,9],[15,7]]
Example 2:

Input: root = [1]
Output: [[1]]
Example 3:

Input: root = []
Output: []
 

Constraints:

The number of nodes in the tree is in the range [0, 2000].
-100 <= Node.val <= 100
```
```cpp
//cpp
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
    vector<vector<int>> zigzagLevelOrder(TreeNode* root) {
        if(root == nullptr){
            return {};
        }
        
        vector<vector<int>> res;
        int flag = 0;
        queue<TreeNode*> dq;
        dq.emplace(root);
        while(!dq.empty()) {
            int count = dq.size();
            vector<int> row(count, 0);
            for(int i = 0; i < count; i++){
                auto elem = dq.front();
                dq.pop();
                row[i] = elem->val;
                if(elem->left != nullptr){
                    dq.emplace(elem->left);
                }
                if(elem->right != nullptr){
                    dq.emplace(elem->right);
                }
            }
            if(flag == 1){
                reverse(begin(row), end(row));
            }
            flag ^= 1;
            res.emplace_back(row);            
        }
        
        return res;
    }
};
```
