# 题目：19. Remove Nth Node From End of List
难度： Medium

## 题目链接：
<https://leetcode.com/problems/remove-nth-node-from-end-of-list/>

## 题目内容：
Given a linked list, remove the n-th node from the end of list and return its head.

Example:

Given linked list: 1->2->3->4->5, and n = 2.

After removing the second node from the end, the linked list becomes 1->2->3->5.
Note:

Given n will always be valid.

Follow up:

Could you do this in one pass?

### 想法：
利用双指针，首先快指针先走n步，接着快指针与慢指针同样走，直到快指针走到了最后一个元素。需要注意一个边界条件：1. 快指针走n步之后，如果快指针为空，那么只需要将head变成head.next。

```
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def removeNthFromEnd(self, head: ListNode, n: int) -> ListNode:
        tmp, tmp1 = head, head
        for i in range(n):
            tmp = tmp.next
        if not tmp:
            return head.next
        
        while tmp.next:
            tmp = tmp.next
            tmp1 = tmp1.next
            
        tmp1.next = tmp1.next.next
        return head
```