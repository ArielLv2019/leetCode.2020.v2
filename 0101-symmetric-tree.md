```
Given a binary tree, check whether it is a mirror of itself (ie, symmetric around its center).

For example, this binary tree [1,2,2,3,4,4,3] is symmetric:

    1
   / \
  2   2
 / \ / \
3  4 4  3
 

But the following [1,2,2,null,3,null,3] is not:

    1
   / \
  2   2
   \   \
   3    3
 

Follow up: Solve it both recursively and iteratively.
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
func isSymmetric(root *TreeNode) bool {
    if root == nil {
        return true
    }
    return dfs(root.Left, root.Right)
}

func dfs(l *TreeNode, r *TreeNode) bool{
    if l == nil && r == nil{
        return true
    }
    
    if l != nil && r != nil{
        if l.Val == r.Val{
            return dfs(l.Left, r.Right) && dfs(l.Right, r.Left)
        }
    }
    
    return false
}
```
