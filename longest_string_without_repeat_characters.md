# 3 Longest Substring Without Repeating Characters

难度： Medium

## 题目内容
<https://leetcode.com/problems/longest-substring-without-repeating-characters/>

## 题目描述
Given a string, find the length of the longest substring without repeating characters.

Example 1:

Input: "abcabcbb"
Output: 3 
Explanation: The answer is "abc", with the length of 3. 
Example 2:

Input: "bbbbb"
Output: 1
Explanation: The answer is "b", with the length of 1.
Example 3:

Input: "pwwkew"
Output: 3
Explanation: The answer is "wke", with the length of 3. 
             Note that the answer must be a substring, "pwke" is a subsequence and not a substring.

### 解题思路：
1.用一个字典记录每个字符值以及对应的位置，以及用一个start指针指示我们检查某段子字符串的开头（比如例题1，当字典记录到第二个a时，start变成了1，前面重复的那段被丢弃）
2.对每个字符都进行判断是否该字符与“前面的字符”有重复，此处前面的字符表示前面的某个区间的字符（有可能不是整个前面的字符串）
3. 将有重复的子字符串的长度与之前的最长不重复子字符串长度进行比较，取最长的
   
```
class Solution:
    def lengthOfLongestSubstring(self, s: str) -> int:
        ls, start = 0, 0
        record = {}
        for i, v in enumerate(s):
            if v in record and record[v] >= start:
                ls = max(ls, i - start)
                start = record[v] + 1
            record[v] = i
            
        return max(ls, len(s) - start)
```
