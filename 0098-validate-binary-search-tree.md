```
Given a binary tree, determine if it is a valid binary search tree (BST).

Assume a BST is defined as follows:

    The left subtree of a node contains only nodes with keys less than the node's key.
    The right subtree of a node contains only nodes with keys greater than the node's key.
    Both the left and right subtrees must also be binary search trees.

Example 1:
    2
   / \
  1   3

Input: [2,1,3]
Output: true

Example 2:
    5
   / \
  1   4
     / \
    3   6

Input: [5,1,4,null,null,3,6]
Output: false
Explanation: The root node's value is 5 but its right child's value is 4.
```
```go
/**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
// 递归
func isValidBST(root *TreeNode) bool {
	if root == nil {
		return true
	}
	return isValidBSTProxy(root, nil, nil)
}

func isValidBSTProxy(root, min, max *TreeNode) bool {
	if root == nil {
		return true
	}
	if min != nil && root.Val <= min.Val { // ==也要返回false
		return false
	}
	if max != nil && root.Val >= max.Val {// ==也要返回false
		return false
	}

	return isValidBSTProxy(root.Left, min, root) && isValidBSTProxy(root.Right, root, max)
}
```

```go
/**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
// 递归 + 中序遍历
func isValidBST(root *TreeNode) bool {
	if root == nil {
		return true
	}
    nums := inorder(root)
    for i := 1; i < len(nums); i++ {
        if nums[i-1] >= nums[i]{
            return false
        } 
    }
    
    return true
}

func inorder(root *TreeNode) []int {
	if root == nil {
		return nil
	}

    return append(append(inorder(root.Left), root.Val), inorder(root.Right)...)
}
```

```cpp
// 递归 + 中序遍历
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
        std::vector<int> vec{};
        
        return inorder(root, vec);
    }
    
    bool inorder(TreeNode* root, std::vector<int>& vec){
        if( root == nullptr ){
            return true;
        }
        
        if( !inorder(root->left, vec) ){
            return false;
        }
        
        if(!vec.empty() && vec.back() >= root->val){
            return false;
        }
        
        vec.emplace_back(root->val);
        return inorder(root->right, vec);
    }
};
```
```cpp
// Iteration: stack
class Solution {
public:
    bool isValidBST(TreeNode* root) {
        if( root == nullptr){
            return true;
        }
        
        std::stack<TreeNode*> s;
        long pre = LONG_MIN;
        // std::vector<int> vec;
        while(!s.empty() || root != nullptr){
            if( root != nullptr){
                s.emplace(root);
                root = root->left;
            }else{
                root = s.top();
                s.pop();
                if( pre >= root->val){
                    return false;
                }
                pre = root->val;
                //if( !vec.empty() && vec.back() >= root->val){
                //    return false;
                //}
                //vec.emplace_back(root->val);
                root = root->right;
            }
        }
        
        return true;
    }
};
```
