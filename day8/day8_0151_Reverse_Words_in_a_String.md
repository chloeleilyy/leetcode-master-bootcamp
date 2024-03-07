# Problem

Given an input string `s`, reverse the order of the **words**.

A **word** is defined as a sequence of non-space characters. The **words** in `s` will be separated by at least one space.

Return *a string of the words in reverse order concatenated by a single space.*

**Note** that `s` may contain leading or trailing spaces or multiple spaces between two words. The returned string should only have a single space separating the words. Do not include any extra spaces.

**Example 1:**

```
Input: s = "the sky is blue"
Output: "blue is sky the"
```

**Example 2:**

```
Input: s = "  hello world  "
Output: "world hello"
Explanation: Your reversed string should not contain leading or trailing spaces.
```

**Example 3:**

```
Input: s = "a good   example"
Output: "example good a"
Explanation: You need to reduce multiple spaces between two words to a single space in the reversed string.
```

 

**Constraints:**

- `1 <= s.length <= 104`
- `s` contains English letters (upper-case and lower-case), digits, and spaces `' '`.
- There is **at least one** word in `s`.

 

**Follow-up:** If the string data type is mutable in your language, can you solve it **in-place** with `O(1)` extra space?



## Classification & Discussion





## Notes

- 还有其他python使用库函数的解法



****

# Solution



### ==Step==

1. 
2. 





## Important details





## Code

- 记得判断index合法在其他判断条件之前
- 先反转每个单词再反转整个字符串
- 使用temp指针在整个列表中游走

```python
class Solution:
    def reverseWords(self, s: str) -> str:
        s = list(s)
        new_s = []
        i, j = 0, len(s) - 1
        # delete leading spaces
        while s[i] == " ":
            i += 1
        # delete trailing spaces
        while s[j] == " ":
            j -= 1
        # reverse each word
        s = s[i:j+1]
        i, temp = 0, 0
        while i < len(s):
            while temp != len(s) and s[temp] != " ":
                temp += 1
            new_s += s[i:temp][::-1]
            if temp != len(s):
                new_s.append(" ")
            while temp != len(s) and s[temp] == " ":
                temp += 1
            i = temp
        # reverse the whole str list
        new_s.reverse()
        return "".join(new_s)


```

## Code 2

- 注意最后一个单词的处理

```python
# 1.使用双指针移除多余的空格
# 2.reverse每个单词
# 3.reverse整个字符串
class Solution:
    def removeExtraSpace(self, s: list) -> list:
        slow = 0
        i = 0
        while i < len(s):
            # 只有在不是空格的时候收集，相当于删除空格
            if s[i] != " ":
                # 在不是首字母的单词前添加空格
                if slow != 0:
                    s[slow] = " "
                    slow += 1
                # 补全整个单词
                while i < len(s) and s[i] != " ":
                    s[slow] = s[i]
                    slow += 1
                    i += 1
            i += 1
        return s[:slow]

    def reverseWords(self, s: str) -> str:
        s = list(s)
        s = self.removeExtraSpace(s)
        # 2.reverse each word
        start, i = 0, 0
        while i <= len(s):
            if i == len(s) or s[i] == " ":
                s[start:i] = s[start:i][::-1]
                start = i + 1
            i += 1
        # 3.reverse the whole string
        print(s)
        s = s[::-1]
        return "".join(s)
```

Time: O(n)

Space: O(n)



## Best Complexity

Time Complexity: O(n)

Space Complexity: O(n)