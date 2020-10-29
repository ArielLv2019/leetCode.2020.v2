```
Given a binary tree, find the lowest common ancestor (LCA) of two given nodes in the tree.

According to the definition of LCA on Wikipedia: “The lowest common ancestor is defined between two nodes p and q as the lowest node in T that has both p and q as descendants (where we allow a node to be a descendant of itself).”


Example 1:
Input: root = [3,5,1,6,2,0,8,null,null,7,4], p = 5, q = 1
Output: 3
Explanation: The LCA of nodes 5 and 1 is 3.

Example 2:
Input: root = [3,5,1,6,2,0,8,null,null,7,4], p = 5, q = 4
Output: 5
Explanation: The LCA of nodes 5 and 4 is 5, since a node can be a descendant of itself according to the LCA definition.

Example 3:
Input: root = [1,2], p = 1, q = 2
Output: 1

Constraints:

    The number of nodes in the tree is in the range [2, 105].
    -109 <= Node.val <= 109
    All Node.val are unique.
    p != q
    p and q will exist in the tree.
```
```
Method 1:
1） 构建从root到p，q的路径
2） 求两个单向链表的第一个非公共节点的问题
```
```
Method 2:
递归求解
```
```go
// 递归
/**
 * Definition for TreeNode.
 * type TreeNode struct {
 *     Val int
 *     Left *ListNode
 *     Right *ListNode
 * }
 */
 func lowestCommonAncestor(root, p, q *TreeNode) *TreeNode {
     if root == nil || root == p || root == q{
         return root
     }
     if q == nil{
         return p
     }
     if p == nil || p == q{
         return q
     }
     
     left := lowestCommonAncestor(root.Left, p, q)
     right := lowestCommonAncestor(root.Right, p, q)
     
     if left != nil && right != nil{
         return root
     }
     if left == nil{
         return right
     }
     return left
}
```

```go
// 找路径+求公共节点
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
        if( root == nullptr || root == p || root == q ){
            return root;
        }
        if( p == nullptr){
            return q;
        }
        if( q == nullptr || p == q ){
            return q;
        }
        
        std::vector<TreeNode*> pPath, qPath;
        FindPath(root, p, pPath);
        FindPath(root, q, qPath);
        
        return FirstLastCommon(pPath, qPath);
    }
    
    bool FindPath(TreeNode* root, TreeNode* p, std::vector<TreeNode*>& vec){
        if( root == nullptr){
            return false;
        }
        if( root == p){
            vec.emplace_back(p);
            return true;
        }
        
        vec.emplace_back(root);
        bool find = FindPath(root->left, p, vec);
        if(!find){
            find= FindPath(root->right, p, vec);
        }
        if(!find){
            vec.pop_back();
        }
        return find;
    }

    TreeNode* FirstLastCommon(std::vector<TreeNode*>& v1, std::vector<TreeNode*>& v2){
        for(int i = std::min(v1.size(), v2.size()) - 1; i >= 0; i--){
            if(v1[i] == v2[i]){
                return v1[i];
            }
        }
        return nullptr;
    }
};

```
