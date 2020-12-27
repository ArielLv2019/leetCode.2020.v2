```
Given a binary search tree, write a function kthSmallest to find the kth smallest element in it.

 

Example 1:

Input: root = [3,1,4,null,2], k = 1
   3
  / \
 1   4
  \
   2
Output: 1
Example 2:

Input: root = [5,3,6,2,4,null,null,1], k = 3
       5
      / \
     3   6
    / \
   2   4
  /
 1
Output: 3
Follow up:
What if the BST is modified (insert/delete operations) often and you need to find the kth smallest frequently? How would you optimize the kthSmallest routine?
```

```cpp
// cpp: vector<int> res
Given a binary search tree, write a function kthSmallest to find the kth smallest element in it.

 

Example 1:

Input: root = [3,1,4,null,2], k = 1
   3
  / \
 1   4
  \
   2
Output: 1
Example 2:

Input: root = [5,3,6,2,4,null,null,1], k = 3
       5
      / \
     3   6
    / \
   2   4
  /
 1
Output: 3
Follow up:
What if the BST is modified (insert/delete operations) often and you need to find the kth smallest frequently? How would you optimize the kthSmallest routine?
```

```cpp
// cpp: Inorder + vector<int>
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
    int kthSmallest(TreeNode* root, int k) {
        vector<int> res;
        
        inOrder(root, res, k);
        return res[k-1];
    }
    
    void inOrder(TreeNode* root, vector<int>& res, int k) {        
        if(res.size() >= k){
            return ;
        }
        if (root->left != nullptr){
            inOrder(root->left, res, k);
        }
        res.emplace_back(root->val);
        if(root->right != nullptr){
            inOrder(root->right, res, k); 
        }
        
        return ;
    }     
};
```

```cpp
// cpp: Inorder
// Go inorder and decrease k at each node. Stop the whole search as soon as k is zero, 
// and then the k-th element is immediately returned all the way to the recursion top and to the original caller.

// Try the left subtree first. If that made k zero, then its answer is the overall answer and we return it right away. 
// Otherwise, decrease k for the current node, and if that made k zero, then we return the current node's value right away. 
// Otherwise try the right subtree and return whatever comes back from there.


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
    int kthSmallest(TreeNode* root, int k) {
        return inOrder(root, k);
    }
    
    int inOrder(TreeNode* root, int& k) {
        if(root != nullptr){
            int leftResult = inOrder(root->left, k);
            return k == 0? leftResult: --k == 0? root->val: inOrder(root->right, k);
        }   
        return -1;
    }     
};
```
