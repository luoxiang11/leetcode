# 4 Median of Two Sorted Arrays
难度： hard

## 题目内容
<https://leetcode.com/problems/median-of-two-sorted-arrays/>

## 题目描述
There are two sorted arrays nums1 and nums2 of size m and n respectively.

Find the median of the two sorted arrays. The overall run time complexity should be O(log (m+n)).

You may assume nums1 and nums2 cannot be both empty.

Example 1:

nums1 = [1, 3]
nums2 = [2]

The median is 2.0
Example 2:

nums1 = [1, 2]
nums2 = [3, 4]

The median is (2 + 3)/2 = 2.5

### 解题思路
对于两个list，A和B。 假设A随机选择i的位置
<center> left A |right A <center>
<center>A[0], ... A[i-1]|A[i]...A[m-1]<center>


B随机选择在j的位置

<center> left B   |   right B <center>
<center>B[0],...B[j-1]|B[j] ... B[n-1]<center>

我们现在希望取到两个有序list的中位数，所以希望i+j 等于 (m+n+1)//2, 从而确定了i+j必须满足这样一个条件，然后再根据二分法就可以大致解决这个问题
```
class Solution:
    def findMedianSortedArrays(self, nums1: List[int], nums2: List[int]) -> float:
        m, n = len(nums1), len(nums2)
        if m > n:
            m, n, nums1, nums2 = n, m, nums2, nums1
        median = (m+n+1)//2
        left, right = 0, m
        while left <= right:
            i = (left+right)//2
            j = median - i
            if i > 0 and nums1[i-1] > nums2[j]:
                right = i-1
            elif i < m and nums1[i] < nums2[j-1]:
                left = i + 1
            else:
                if i == 0:
                    leftmax = nums2[j-1]
                elif j == 0:
                    leftmax = nums1[i-1]
                else:
                    leftmax = max(nums1[i-1], nums2[j-1])
                    
                if (m+n) % 2:
                    return leftmax

                else:
                    if i == m:
                        rightmin= nums2[j]
                    elif j == n:
                        rightmin = nums1[i]
                    else:
                        rightmin = min(nums1[i], nums2[j])
                        
                        
                    return (leftmax + rightmin) / 2.0
```