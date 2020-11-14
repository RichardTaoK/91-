# Day 04

## 题目(394.字符串解码)

```
给定一个经过编码的字符串，返回它解码后的字符串。

编码规则为: k[encoded_string]，表示其中方括号内部的 encoded_string 正好重复 k 次。注意 k 保证为正整数。

你可以认为输入字符串总是有效的；输入字符串中没有额外的空格，且输入的方括号总是符合格式要求的。

此外，你可以认为原始数据不包含数字，所有的数字只表示重复的次数 k ，例如不会出现像 3a 或 2[4] 的输入。

 

示例 1：

输入：s = "3[a]2[bc]"
输出："aaabcbc"
示例 2：

输入：s = "3[a2[c]]"
输出："accaccacc"
示例 3：

输入：s = "2[abc]3[cd]ef"
输出："abcabccdcdcdef"
示例 4：

输入：s = "abc3[cd]xyz"
输出："abccdcdcdxyz"
```

## 题解

```python
class Solution:
    def decodeString(self, s: str) -> str:
        stack=[]
        for c in s:
            #一直入栈直到出现]就说明要出栈了，直到出栈为不是数字然后将重复完的再入栈
            if c==']':
                strrepeat=''
                strcount=''
                while stack and stack[-1]!='[':#栈顶不为[就一直出栈
                    strrepeat=stack.pop()+strrepeat
                stack.pop()#将[出栈
                while stack and stack[-1].isnumeric():
                    strcount = stack.pop() + strcount#防止出现两位数或者三位数的重复数字
                stack.append(strrepeat*int(strcount))
            else:
                stack.append(c)
        return ''.join(stack)
```

## 复杂度分析

- 时间复杂度 `O(N)`,其中N为循环一趟的结果
- 空间复杂度`O(N)`,为栈的最大空间