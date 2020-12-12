```
Given a root node reference of a BST and a key, delete the node with the given key in the BST.
Return the root node reference (possibly updated) of the BST.

Basically, the deletion can be divided into two stages:

Search for a node to remove.
If the node is found, delete the node.
Follow up: Can you solve it with time complexity O(height of tree)?

 
Example 1:
Input: root = [5,3,6,2,4,null,7], key = 3
Output: [5,4,6,2,null,null,7]
Explanation: Given key to delete is 3. So we find the node with value 3 and delete it.
One valid answer is [5,4,6,2,null,null,7], shown in the above BST.
Please notice that another valid answer is [5,2,6,null,4,null,7] and it's also accepted.

Example 2:
Input: root = [5,3,6,2,4,null,7], key = 0
Output: [5,3,6,2,4,null,7]
Explanation: The tree does not contain a node with value = 0.

Example 3:
Input: root = [], key = 0
Output: []
```

```cpp
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
    TreeNode* deleteNode(TreeNode* root, int key) {
        TreeNode* p = root, *pp = nullptr; // pp记录父亲节点
        while(p != nullptr && p->val != key){
            pp = p;
            if(p->val > key){
                p = p->left;
            }else{
                p = p->right;
            }
        }
        if( p == nullptr ){ //没有找到节点
            return root;
        }
        
        //删除的节点有两个字节点
        if(p->left != nullptr && p->right != nullptr){
            TreeNode *minP = p->right, *minPp = p; //minPp是右子树最左节点的父jiedian
            while(minP->left != nullptr){
                minPp = minP;
                minP = minP->left;
            }
            
            p->val = minP->val; //将minP中的数据 -> p节点中
            p = minP; //换成删除minP
            pp = minPp;
        }
        
        TreeNode* child = nullptr; 
        if(p->left != nullptr){ //只有左子树
            child = p->left;
        }else if(p->right != nullptr) { //只有右子树
            child = p->right;
        }
        
        if (pp == nullptr){ //要删除的是根节点
            root = child;
        }else{
            if(pp->left == p){ //p是父节点的左孩子
                pp->left = child;
            }else{
                pp->right = child;
            }
        }
        
        return root;
    }
};
```
