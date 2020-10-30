```
Given a binary tree, find its minimum depth.

The minimum depth is the number of nodes along the shortest path from the root node down to the nearest leaf node.

Note: A leaf is a node with no children.


Example 1:
Input: root = [3,9,20,null,null,15,7]
Output: 2

Example 2:
Input: root = [2,null,3,null,4,null,5,null,6]
Output: 5
```
```cpp
// 递归
class Solution {
public:
    int minDepth(TreeNode* root) {
        if (root == nullptr){
            return 0;
        }
        if( root->left == nullptr){
            return 1 + minDepth(root->right);
        }
        if( root->right == nullptr){
            return 1 + minDepth(root->left);
        }
        
        return 1 + min(minDepth(root->left), minDepth(root->right));
    }
};
```
```cpp
//递归2
class Solution {
public:
    int minDepth(TreeNode* root) {
        if (root == nullptr){
            return 0;
        }
        
        int leftDepth = 0, rightDepth = 0;
        if(root->left != nullptr){
            leftDepth = minDepth(root->left);
        }
        if(root->right != nullptr){
            rightDepth = minDepth(root->right);
        }
         
        return (leftDepth == 0 ||rightDepth ==0)
            ? 1+leftDepth+rightDepth 
            : 1 + min(leftDepth, rightDepth);
    }
};
```
