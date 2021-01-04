```
You are given two non-empty linked lists representing two non-negative integers. The digits are stored in reverse order, and each of their nodes contains a single digit. Add the two numbers and return the sum as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

 

Example 1:


Input: l1 = [2,4,3], l2 = [5,6,4]
Output: [7,0,8]
Explanation: 342 + 465 = 807.
Example 2:

Input: l1 = [0], l2 = [0]
Output: [0]
Example 3:

Input: l1 = [9,9,9,9,9,9,9], l2 = [9,9,9,9]
Output: [8,9,9,9,0,0,0,1]
```
```go
//go
/**
 * Definition for singly-linked list.
 * type ListNode struct {
 *     Val int
 *     Next *ListNode
 * }
 */
func addTwoNumbers(l1 *ListNode, l2 *ListNode) *ListNode {
    dummyHead := ListNode{}
    pre := &dummyHead
    carry := 0
    for ; l1 != nil && l2 != nil; l1, l2, pre = l1.Next, l2.Next, pre.Next{
        sum := carry + l1.Val + l2.Val
        if sum >= 10{
            pre.Next = &ListNode{Val: sum % 10}
            carry = sum / 10
        }else{
            pre.Next = &ListNode{Val: sum}
            carry = 0
        }        
    }
    cur := l1
    if l1 == nil{
        cur = l2
    }
    for ; cur != nil; cur, pre = cur.Next, pre.Next{
        sum := carry + cur.Val
        if sum >= 10{
            pre.Next = &ListNode{Val: sum % 10}
            carry = sum / 10
        }else{
            pre.Next = &ListNode{Val: sum}
            carry = 0
        }        
    }
    if carry > 0{
        pre.Next = &ListNode{Val:carry}
    }
     
    return dummyHead.Next
}
```
