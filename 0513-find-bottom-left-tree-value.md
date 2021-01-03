```
Given the root of a binary tree, return the leftmost value in the last row of the tree.

Example 1:
Input: root = [2,1,3]
Output: 1

Example 2:
Input: root = [1,2,3,4,null,5,6,null,null,7]
Output: 7
```
```go
// go + dfs
/**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
func findBottomLeftValue(root *TreeNode) int {
    if root == nil{
        return -1
    }
    
    res, maxDepth := root.Val, 1  
    dfs(root, 1, &maxDepth, &res)
    
    return res
}

func dfs(root *TreeNode, depth int, maxDepth, res *int){
    if root == nil{
        return
    }
    if depth > *maxDepth{
        *maxDepth = depth
        *res = root.Val
    }
    
    dfs(root.Left, depth+1, maxDepth, res)
    dfs(root.Right, depth+1, maxDepth, res)
    
    return 
}
```

```cpp
// dpp + BFS + deque
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
    int findBottomLeftValue(TreeNode* root) {
        if(root == nullptr){
            return -1;
        }
        deque<pair<TreeNode*, int>> dq;
        dq.emplace_back(make_pair(root, 1));
        int res = root->val, depth = 1;        
        while(!empty(dq)){
            auto cur = dq.front();
            dq.pop_front();
            if (cur.second > depth){
                depth = cur.second;
                res = cur.first->val;
            }
            if(cur.first->left != nullptr) {
                dq.emplace_back(make_pair(cur.first->left, cur.second+1));
            }
            if(cur.first->right != nullptr){
                dq.emplace_back(make_pair(cur.first->right, cur.second+1));
            }
        }
        return res;
    }
};
```
