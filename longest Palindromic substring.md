# 5. Longest Palindromic Substring
难度： Medium

## 题目链接
<https://leetcode.com/problems/longest-palindromic-substring/>

## 题目内容
Given a string s, find the longest palindromic substring in s. You may assume that the maximum length of s is 1000.

Example 1:

Input: "babad"
Output: "bab"
Note: "aba" is also a valid answer.
Example 2:

Input: "cbbd"
Output: "bb"

### 想法：
1. 利用图表法：
   1. 首先用一个n乘以n的list记录长度为n的string的任意长度的substring的是否为Palindromic substring。
   2. 利用动态规划的bottom up的想法，
      1. 第一步，对于所有长度为1的子序列，都是Palindromic子序列，用TRUE表示
      2. 对于长度为2的子序列，判断两个元素是否相等，如果相等，则对应的图标记录变成True
      3. 对于成都为3一直到n的子序列，如果子序列是Palindromic substring,则第一个元素等于最后一个元素，并且第二个元素至倒数第二个元素也是一个Palindromic subtring，于是找到了递归条件
代码如下：
```
class Solution:
    def longestPalindrome(self, s: str) -> str:
        n = len(s)
        dp = [[False]*n for i in range(n)]
        start, l = 0, 0
        for i in range(n):
            dp[i][i] = True
        for i in range(n-1):
            j = i+1
            if s[i] == s[j]:
                dp[i][j] = True
                start = i
                l = 1
        
        
        for length in range(2, n):
            for i in range(n-length):
                if s[i] == s[i+length] and dp[i+1][i+length-1]:
                    dp[i][i+length] = True
                    start = i
                    l = length
                    
        return s[start:start+l+1]
                
```


2. 递归方法：
   对任何一个palindrome子序列，要么是关于中心对称，要么是关于中间两个相等的元素对称，并且所有的palindrome子序列的都满足这样的性质，我们可以定义一个判断panlindrome子序列长度的函数，然后关于所有的一个与相邻两个元素的情况进行函数遍历，选择长度最长的

代码：
```
class Solution:
    def longestPalindrome(self, s: str) -> str:
        def check_palindrome(s, start, end):
            while start >=0 and end < len(s) and s[start] == s[end]:
                start -= 1
                end += 1
            return end - start -1
        
        n = len(s)
        start, end = 0, 0
        for i in range(n):
            l1 = check_palindrome(s,i,i)
            l2 = check_palindrome(s,i,i+1)
            l = max(l1, l2)
            if l > end - start:
                start = i - (l-1)// 2
                end = l // 2 + i
                
        return s[start : end +1]
```
