# 题目： 21. Merge Two Sorted Lists
难度： Easy

## 题目链接：
<https://leetcode.com/problems/merge-two-sorted-lists/>

## 题目描述：
Merge two sorted linked lists and return it as a new list. The new list should be made by splicing together the nodes of the first two lists.

Example:

Input: 1->2->4, 1->3->4
Output: 1->1->2->3->4->4

### 想法：
初始化两个相同的指针，让一个指针按大小顺序记录

```
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def mergeTwoLists(self, l1: ListNode, l2: ListNode) -> ListNode:
        l = head = ListNode(0)
        
        while l1 and l2:
            if l1.val > l2.val:
                l.next = ListNode(l2.val)
                l2 = l2.next
            else:
                l.next = ListNode(l1.val)
                l1 = l1.next
            l = l.next
        l.next = l1 or l2
        l = l.next
        return head.next
```