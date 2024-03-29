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
```cpp
// cpp: stack + pPre pointer
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
        if(root == nullptr){
            return true;
        }
        
        stack<TreeNode*> sta;
        TreeNode* pPre = nullptr;
        while(root != nullptr || !sta.empty()){
            while(root != nullptr){
                sta.emplace(root);
                root = root->left;
            }
            root = sta.top();
            sta.pop();
            if(pPre != nullptr && pPre->val >= root->val){
                return false;
            }
            pPre = root;
            root = root->right;
            
        }
        
        return true;
    }
};
```
```cpp
//cpp: recurie + min + max
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
        if(root == nullptr){
            return true;
        }
        
        return isValidBST(root, nullptr, nullptr);
    }
    
    bool isValidBST(TreeNode* root,TreeNode *pMin,TreeNode *pMax) {
        if(root == nullptr){
            return true;
        }
        if(pMin != nullptr && pMin->val >= root->val){
            return false;
        }
        if(pMax != nullptr && pMax->val <= root->val){
            return false;
        }
        return isValidBST(root->left, pMin,root) && isValidBST(root->right, root, pMax) ;
    }
    
};
```
```cpp
//cpp: recurite + &pPre
// 最快
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
        if(root == nullptr){
            return true;
        }
        
        TreeNode *pPre = nullptr;
        
        return isValidBST(root, pPre);
    }
    
    bool isValidBST(TreeNode* root,TreeNode* &pPre) {
        if(root == nullptr){
            return true;
        }
        if(!isValidBST(root->left, pPre)){
            return false;
        }
        if(pPre != nullptr && pPre->val >= root->val){
            return false;
        }
        pPre = root;
        return isValidBST(root->right, pPre);
    }
    
};
```
```go
// go
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
// go: 递归 + 中序遍历
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
```go
// go + stack
/**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
const INT_MAX = int(^uint(0)>>1)
const INT_MIN = ^INT_MAX
func isValidBST(root *TreeNode) bool {
    if root == nil || 
    (root.Left == nil && root.Right == nil) {
        return true
    }
    
    pre := INT_MIN
    sta := []*TreeNode{}
    for len(sta) > 0 || root != nil{
        if root != nil{
            sta = append(sta, root)
            root = root.Left
        }else{
            root = sta[len(sta)-1]
            sta = sta[0:len(sta)-1]
            if pre >= root.Val{
                return false
            }
            pre = root.Val
            root = root.Right
        }
    }
    
    return true
}
```
```cpp
// cpp: 递归 + 中序遍历
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
  
