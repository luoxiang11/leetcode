#  11.Container With Most Water
难度： Medium

## 题目链接
<https://leetcode.com/problems/container-with-most-water/>

## 题目内容：
Given n non-negative integers a1, a2, ..., an , where each represents a point at coordinate (i, ai). n vertical lines are drawn such that the two endpoints of line i is at (i, ai) and (i, 0). Find two lines, which together with x-axis forms a container, such that the container contains the most water.

Note: You may not slant the container and n is at least 2.
Example:

Input: [1,8,6,2,5,4,8,3,7]
Output: 49

### 想法：
对于一个宽度固定的长度不相等的形状体，它所能装的水由最短的边所决定，对于本题的情形，首尾宽的形状体已经给出了所能装水的最大面积的一个下限，并且如果还想找到面积比这个形状体更大的形状体，最短的边一定会比首尾两条边最短的长，因为宽度一定小于首尾形状体的宽度，从而只需要首尾两个指针进行操作。

代码：
```
class Solution:
    def maxArea(self, height: List[int]) -> int:
        n = len(height)
        left, right = 0, n-1
        maxarea = float("-inf")
        while left < right:
            if height[left] > height[right]:
                minheight = height[right]
                right -= 1
            else:
                minheight = height[left]
                left += 1
                
            maxarea = max(maxarea, (right - left +1) * minheight)
            
        return maxarea
```