# 10. Regular Expression Matching
难度： Hard

## 题目链接：
<https://leetcode.com/problems/regular-expression-matching/>

## 题目内容：
Given an input string (s) and a pattern (p), implement regular expression matching with support for '.' and '*'.

'.' Matches any single character.
'*' Matches zero or more of the preceding element.
The matching should cover the entire input string (not partial).

Note:

s could be empty and contains only lowercase letters a-z.
p could be empty and contains only lowercase letters a-z, and characters like . or *.
Example 1:

Input:
s = "aa"
p = "a"
Output: false
Explanation: "a" does not match the entire string "aa".
Example 2:

Input:
s = "aa"
p = "a*"
Output: true
Explanation: '*' means zero or more of the preceding element, 'a'. Therefore, by repeating 'a' once, it becomes "aa".
Example 3:

Input:
s = "ab"
p = ".*"
Output: true
Explanation: ".*" means "zero or more (*) of any character (.)".
Example 4:

Input:
s = "aab"
p = "c*a*b"
Output: true
Explanation: c can be repeated 0 times, a can be repeated 1 time. Therefore, it matches "aab".
Example 5:

Input:
s = "mississippi"
p = "mis*is*p*."
Output: false

### 想法：
1. 首先边界条件：如果p是空的，则结果是否s
2. 用图表法，对任意的i小于s的长度，j小于p的长度，用True表示s[:i+1] 与p[:j+1]是匹配的，用False表示它们不匹配。此处我们用dp[0][0]表示当s,p为空的时候为True。
3. s[:i+1] 与p[:j+1]是匹配只会在两种情况下出现
   1. p[j-1] 属于 [s[i-1], '.']时，有 dp[i][j] = dp[i-1][j-1]
   2. j >=2, p[j-1]等于'*',这时有可能出现两种情况
      1. p[j-2] 属于 [s[i-1], '.'],这时dp[i][j] = dp[i][j-2] or dp[i-1][j](利用了*可以将前面一个元素变0也可以将前面一个元素复制任意次数遍))
      2. dp[i][j] = dp[i][j-2] 利用*将前面元素去掉

代码：
```
class Solution:
    def isMatch(self, s: str, p: str) -> bool:
        if not p:
            return not s
        m, n = len(s), len(p)
        dp = [[False]*(n+1) for i in range(m+1)]
        dp[0][0] = True
        for i in range(2, n+1):
            if p[i-1] == '*':
                dp[0][i] = dp[0][i-2]
        
        for i in range(1, m+1):
            for j in range(1, n+1):
                if p[j-1] in [s[i-1], '.']:
                    dp[i][j] = dp[i-1][j-1]
                elif j >= 2 and p[j-1] == '*':
                    if p[j-2] in [s[i-1], '.']:
                        dp[i][j] = dp[i][j-2] or dp[i-1][j]
                    else:
                        dp[i][j] = dp[i][j-2]
                        
                else:
                    dp[i][j] = False
                    
                    
        return dp[m][n]
```