```
Invert a binary tree.

Example:

Input:

     4
   /   \
  2     7
 / \   / \
1   3 6   9
Output:

     4
   /   \
  7     2
 / \   / \
9   6 3   1
Trivia:
This problem was inspired by this original tweet by Max Howell:

Google: 90% of our engineers use the software you wrote (Homebrew), but you can’t invert a binary tree on a whiteboard so f*** off.
```
```go
// go: 递归
/**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
func invertTree(root *TreeNode) *TreeNode {
    if root == nil || (root.Left == nil && root.Right == nil){
        return root
    } 
    left, right := invertTree(root.Left),  invertTree(root.Right)
    root.Left, root.Right = right, left
    
    return root
}
```

```go
// go + deque
/**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
func invertTree(root *TreeNode) *TreeNode {
    if root == nil || (root.Left == nil && root.Right == nil){
        return root
    } 
    q := []*TreeNode{root}
    for len(q) > 0{
        q[0].Left, q[0].Right =q[0].Right, q[0].Left         
        if q[0].Left != nil{
            q = append(q, q[0].Left)
        }
        if q[0].Right != nil{
            q = append(q, q[0].Right)
        }
        q = q[1:]
    }
    
    return root
}
```
