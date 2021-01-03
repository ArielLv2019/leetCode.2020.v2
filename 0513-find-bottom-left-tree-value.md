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
