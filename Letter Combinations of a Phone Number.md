# 17. Letter Combinations of a Phone Number
难度： Medium

## 题目链接
<https://leetcode.com/problems/letter-combinations-of-a-phone-number/>

## 题目内容：
Given a string containing digits from 2-9 inclusive, return all possible letter combinations that the number could represent.

A mapping of digit to letters (just like on the telephone buttons) is given below. Note that 1 does not map to any letters.


![Alt text](http://upload.wikimedia.org/wikipedia/commons/thumb/7/73/Telephone-keypad2.svg/200px-Telephone-keypad2.svg.png)

Example:

Input: "23"
Output: ["ad", "ae", "af", "bd", "be", "bf", "cd", "ce", "cf"].

### 想法：
直觉想到利用深度优先搜索算法

```
class Solution:
    def letterCombinations(self, digits: str) -> List[str]:
        if not digits:
            return []
        
        dict_mapping = {'2':'abc', '3':'def', '4':'ghi', '5':'jkl', '6':'mno', '7':'pqrs', '8':'tuv',                                   '9':'wxyz'}
        n, res = len(digits), []
        
        def dfs(i, tmp):
            if i == n:
                res.append(tmp)
                return
            else:
                for p in dict_mapping[digits[i]]:
                    dfs(i+1, tmp+p)
        
        dfs(0, '')
        return res
```