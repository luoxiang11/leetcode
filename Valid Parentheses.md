# 20. Valid Parentheses
难道： Easy

## 题目链接:
<https://leetcode.com/problems/valid-parentheses/>

## 题目内容：
Given a string containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.

An input string is valid if:

1. Open brackets must be closed by the same type of brackets.
2. Open brackets must be closed in the correct order.

Note that an empty string is also considered valid.

Example 1:

Input: "()"
Output: true
Example 2:

Input: "()[]{}"
Output: true
Example 3:

Input: "(]"
Output: false
Example 4:

Input: "([)]"
Output: false
Example 5:

Input: "{[]}"
Output: true

### 想法：
利用栈的方法，并且排除几种False的情况。

```
class Solution:
    def isValid(self, s: str) -> bool:
        dict_mapping = {')':'(', ']':'[', '}':'{'}
        stack = []
        
        for i in s:
            if i not in dict_mapping:
                stack.append(i)
            else:
                if not stack:
                    return False
                else:
                    tmp = stack.pop()
                    if tmp != dict_mapping[i]:
                        return False
                    
        return not stack
```