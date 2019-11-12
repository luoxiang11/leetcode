# 15. 3Sum
难度： Medium

## 题目链接:
<https://leetcode.com/problems/3sum/>

## 题目内容：
Given an array nums of n integers, are there elements a, b, c in nums such that a + b + c = 0? Find all unique triplets in the array which gives the sum of zero.

Note:

The solution set must not contain duplicate triplets.

Example:

Given array nums = [-1, 0, 1, 2, -1, -4],

A solution set is:
[
  [-1, 0, 1],
  [-1, -1, 2]
]


### 想法：
首先将数组排序，不排序很难排除相同的三个数字。排序之后首先要注意相同的数字如果能满足条件，一定是重复出现了，所以要注意这个边界条件，其他的主要是基于第一题two sums的方法，但是任然需要注意重复的情况。

```
class Solution:
    def threeSum(self, nums: List[int]) -> List[List[int]]:
        nums.sort()
        n, res = len(nums), []
        
        for i, v in enumerate(nums[:-2]):
            if i > 0 and v == nums[i-1]:
                continue
            tmp = {}
            j = i+1
            while j < n:
                if nums[j] in tmp:
                    res.append([v, -v-nums[j], nums[j]])
                    while j < n-1 and nums[j] == nums[j+1]:
                        j += 1
                else:
                    tmp[-v-nums[j]] = j
                j += 1    
        return res
```