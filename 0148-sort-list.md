```
Given the head of a linked list, return the list after sorting it in ascending order.

Follow up: Can you sort the linked list in O(n logn) time and O(1) memory (i.e. constant space)?


Example 1:
Input: head = [4,2,1,3]
Output: [1,2,3,4]

Example 2:
Input: head = [-1,5,3,4,0]
Output: [-1,0,3,4,5]

Example 3:
Input: head = []
Output: []
```

```cpp
// merge sort
// T(n) = O(nlogn)
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */
class Solution {
public:
    ListNode* sortList(ListNode* head) {
        if(head == nullptr || head->next == nullptr){
            return head;
        }
        
        ListNode* pMid = splitList(head);   
        return mergeList(sortList(head), sortList(pMid));
    }
    
    ListNode* splitList(ListNode* head){
        ListNode* pre = nullptr;
        ListNode* slow = head, *fast = head;
        while(fast != nullptr && fast->next != nullptr){
            pre = slow;
            slow = slow->next;
            fast = fast->next->next;
        }
        if (pre != nullptr){
            pre->next = nullptr;
        }
        return slow;
    }
    
    ListNode* mergeList(ListNode* head1, ListNode* head2){
        if(head1 == nullptr){
            return head2;
        }
        if(head2 == nullptr){
            return head1;
        }
        ListNode* dummyHead = new ListNode(0);
        ListNode* pre = dummyHead;
        while(head1 != nullptr && head2 != nullptr){
            if(head1->val < head2->val){
                pre->next = head1;
                head1 = head1->next;
            }else{
                pre->next = head2;
                head2 = head2->next;
            }
            pre = pre->next;
        }
        if(head1 != nullptr){
            pre->next = head1;
        }
        if(head2 != nullptr){
            pre->next = head2;
        }
        
        return dummyHead->next;
    }
};
```

```cpp
// select sort
// T(n) = O(n^2)
// leetcode会超时空

/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */
class Solution {
public:
    ListNode* sortList(ListNode* head) {
        if(head == nullptr || head->next == nullptr){
            return head;
        }
    
        ListNode* cur = head;
        while( cur != nullptr ){
            ListNode *pMin = cur, *iter = cur;
            while(iter != nullptr){
                if(iter->val < pMin->val){
                    pMin = iter;
                }
                iter = iter->next;
            }
            swap(cur->val, pMin->val);
            cur = cur->next;
        }
               
        return head;
    }
};
```
