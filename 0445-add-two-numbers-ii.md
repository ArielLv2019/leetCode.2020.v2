```
You are given two non-empty linked lists representing two non-negative integers. The most significant digit comes first and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

Follow up:
What if you cannot modify the input lists? In other words, reversing the lists is not allowed.

Example:

Input: (7 -> 2 -> 4 -> 3) + (5 -> 6 -> 4)
Output: 7 -> 8 -> 0 -> 7
```
```go
// go + stack
/**
 * Definition for singly-linked list.
 * type ListNode struct {
 *     Val int
 *     Next *ListNode
 * }
 */
func convToArr(head1 *ListNode)[]int{
    arr1 := []int{}
    for ; head1 != nil; head1 = head1.Next{
        arr1 = append(arr1, head1.Val)
    }
    
    return arr1
}
func addTwoNumbers( head1 *ListNode ,  head2 *ListNode ) *ListNode {
    // write code here
    if head1 == nil{
        return head2
    }
    if head2 == nil{
        return head1
    }
    
    arr1, arr2:= convToArr(head1),convToArr(head2) 
    maxLen := len(arr1)
    if len(arr2) > maxLen{
        maxLen = len(arr2)
    }
    res := make([]int, maxLen)
    carry := 0
    i, j, k := len(arr1) - 1, len(arr2)-1, len(res)-1
    for ; i >= 0 && j >= 0; i, j, k = i-1, j-1, k-1{
        sum := arr1[i] + arr2[j] + carry
        res[k], carry = sum % 10, sum / 10
    }
    if i < 0 {
        i, arr1 = j, arr2
    }
    for ; i >= 0; i, k = i-1, k-1 {
        sum := arr1[i] + carry
        res[k], carry = sum % 10, sum / 10
    }
    dummyHead := ListNode{}
    pre := &dummyHead
    if carry > 0 {
        dummyHead.Next = &ListNode{Val: carry}
        pre = dummyHead.Next
    }
    for i := 0; i < len(res); i, pre = i+1, pre.Next{
        pre.Next = &ListNode{Val: res[i]}
    }
    
    return dummyHead.Next
}
```

```go
// go + reverse
/**
 * Definition for singly-linked list.
 * type ListNode struct {
 *     Val int
 *     Next *ListNode
 * }
 */

func reverseList(head *ListNode)*ListNode{
    if head == nil{
        return nil
    }
    dummyHead := ListNode{}
    for head != nil {
       dummyHead.Next, head, head.Next = head, head.Next, dummyHead.Next
    }
    return dummyHead.Next
}

func addTwoNumbers(head1 *ListNode, head2 *ListNode) *ListNode {
    // write code here
    if head1 == nil{
        return head2
    }
    if head2 == nil{
        return head1
    }
    
    carry := 0
    dummyHead := ListNode{}
    pre := &dummyHead
    head1 = reverseList(head1)
    head2 = reverseList(head2)
    for ; head1 != nil && head2 != nil; head1, head2 = head1.Next, head2.Next{
        sum := head1.Val + head2.Val + carry
        
        pre.Next = &ListNode{
            Val: sum % 10,
        }
        pre, carry = pre.Next, sum / 10
    }
    cur := head1
    if head2 != nil{
        cur = head2
    }
    for ; cur != nil; cur = cur.Next {
        sum := cur.Val + carry
        
        pre.Next = &ListNode{
            Val: sum % 10,
        }
        pre, carry = pre.Next, sum / 10
    }
    if carry > 0{
        pre.Next = &ListNode{ Val: carry}
    }
    
    return reverseList(dummyHead.Next) 
}
```
