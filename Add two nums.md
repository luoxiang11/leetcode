# 2. Add Two Numbers
难度： medium

## 题目内容：
<https://leetcode.com/problems/add-two-numbers/>

## 题目描述
You are given two non-empty linked lists representing two non-negative integers. The digits are stored in reverse order and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

Example:

Input: (2 -> 4 -> 3) + (5 -> 6 -> 4)
Output: 7 -> 0 -> 8
Explanation: 342 + 465 = 807.

### 解题思路：
这个题目有点类似两个大数的加法，主要需要注意的是两个数相加之和大于10的这个情况，用一个叫rem的变量来表示是否之前两个数相加大于10。 时间复杂度为O(m+n),其中m,n分别表示两个指针的长度，空间复杂度也是O(m+n)

```
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def addTwoNumbers(self, l1: ListNode, l2: ListNode) -> ListNode:
        head = l = ListNode(0)
        rem, total_sum = 0, 0
        while l1 or l2:
            total_sum = (l1.val if l1 else 0) + (l2.val if l2 else 0) + rem
            if total_sum >= 10:
                rem = 1
                total_sum -= 10
            else:
                rem = 0
            
            l.next = ListNode(total_sum)
            l = l.next
            
            l1 = l1.next if l1 else None
            l2 = l2.next if l2 else None
            
        if rem:
            l.next = ListNode(1)
            l = l.next
            
        return head.next
        
```