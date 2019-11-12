# 题目： 22. Generate Parentheses
难度： Medium

## 题目链接：
<https://leetcode.com/problems/generate-parentheses/>

## 题目内容：

Given n pairs of parentheses, write a function to generate all combinations of well-formed parentheses.

For example, given n = 3, a solution set is:

[
  "((()))",
  "(()())",
  "(())()",
  "()(())",
  "()()()"
]

### 题目想法：

1. 将'()'看成一个整体，当n等于1时，就是一个括号，当n等于2时，相当于将一个整体括号插入了'('后面，一个插入了')'后面，类似的不管n等于几只是将一个整体括号插入了之前的一个括号组合里面

```
class Solution:
    def generateParenthesis(self, n: int) -> List[str]:
        res = set()
        
        def dfs(i, tmp):
            if i == n:
                res.add(tmp)
                return
            if i == 0:
                dfs(i+1, tmp+'()')
            else:
                for j, v in enumerate(tmp):
                    dfs(i+1, tmp[:j+1] +'()' +tmp[j+1:])
                    
        dfs(0, '')
        return res
```
这种方法时间复杂度很高，最糟糕时可以达到 n！。

2.任然是backtracking 方法，我们可以观察到，'(' 与')'的个数都等于n，并且对任意的子序列而言都是'('的个数大于等于')'的个数。可以利用这个观察将时间复杂度降低很多

```
class Solution:
    def generateParenthesis(self, N: int) -> List[str]:
        ans = []
        def backtrack(S = '', left = 0, right = 0):
            if len(S) == 2 * N:
                ans.append(S)
                return
            if left < N:
                backtrack(S+'(', left+1, right)
            if right < left:
                backtrack(S+')', left, right+1)

        backtrack()
        return ans
```