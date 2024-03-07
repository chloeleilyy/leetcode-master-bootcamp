# Problem

https://leetcode.cn/problems/string-to-url-lcci/description/

https://leetcode.cn/problems/string-to-url-lcci/description/



URL化。编写一种方法，将字符串中的空格全部替换为`%20`。假定该字符串尾部有足够的空间存放新增字符，并且知道字符串的“真实”长度。（注：用`Java`实现的话，请使用字符数组实现，以便直接在数组上操作。）

 

**示例 1：**

```
输入："Mr John Smith    ", 13
输出："Mr%20John%20Smith"
```

**示例 2：**

```
输入："               ", 5
输出："%20%20%20%20%20"
```

 

**提示：**

- 字符串长度在 [0, 500000] 范围内。







## Classification & Discussion





## Notes

- replace function 的 time complexity 不确定



****

# Solution

从前向后填充就是O(n^2)的算法了，因为每次添加元素都要将添加元素之后的所有元素整体向后移动。

**其实很多数组填充类的问题，其做法都是先预先给数组扩容带填充后的大小，然后在从后向前进行操作。**

这么做有两个好处：

1. 不用申请新数组。
2. 从后向前填充元素，避免了从前向后填充元素时，每次添加元素都要将添加元素之后的所有元素向后移动的问题。

### ==Step==

1. 
2. 





## Important details

- 需要先统计需要的新长度



## Code

```python
class Solution:
    def replaceSpaces(self, S: str, length: int) -> str:
        s = list(S)
        n = len(s)
        # from right to left
        count = 0
        for k in range(length):
            if s[k] == " ":
                count += 1
        new_length = length + count * 2
        i = new_length -1
        j = length - 1 
        while j >= 0 and i >= 0:
            if s[j] != " ":
                s[i] = s[j]
                i -= 1
                j -= 1
            else:
                s[i] = "0"
                s[i - 1] = "2"
                s[i - 2] = "%"
                j -= 1
                i -= 3
        return "".join(s[:new_length])
# time:O(n)
# space:O(n), use list
```



```python
class Solution:
    def replaceSpaces(self, S: str, length: int) -> str:
        new_str = S[:length]
        return new_str.replace(" ", "%20")
    
# time: 
# space: 
```



The time complexity of Python’s `str.replace()` function can be a bit complex to understand because it depends on several factors.

[The `str.replace()` function in Python is based on the Boyer–Moore algorithm](https://stackoverflow.com/questions/66163149/does-str-replace-have-a-time-complexity-on2)[1](https://stackoverflow.com/questions/66163149/does-str-replace-have-a-time-complexity-on2). [The worst-case time complexity of this algorithm is O(n*m), where ‘n’ is the length of the string and ‘m’ is the length of the substring](https://stackoverflow.com/questions/66163149/does-str-replace-have-a-time-complexity-on2)[1](https://stackoverflow.com/questions/66163149/does-str-replace-have-a-time-complexity-on2).

However, when we consider multiple replacements, the time complexity can potentially increase. If the function can only replace one substring at a time, then for a single substring we get O(n*m), times the number of substrings which is a maximum of n/m. [This comes to O(n^2)](https://stackoverflow.com/questions/66163149/does-str-replace-have-a-time-complexity-on2)[1](https://stackoverflow.com/questions/66163149/does-str-replace-have-a-time-complexity-on2)[2](https://stackoom.com/en/question/4Tc3Z).

[But, there’s a more detailed analysis that suggests the worst case is O(n*(m1 + m2/m1)) where n is the length of the string, m1 is the length of the searched for string and m2 is the length of the replacement](https://stackoverflow.com/questions/66163149/does-str-replace-have-a-time-complexity-on2)[1](https://stackoverflow.com/questions/66163149/does-str-replace-have-a-time-complexity-on2). [The average case is O(n * (1 + m2/m1))](https://stackoverflow.com/questions/66163149/does-str-replace-have-a-time-complexity-on2)[1](https://stackoverflow.com/questions/66163149/does-str-replace-have-a-time-complexity-on2).

It’s important to note that these are theoretical complexities and actual performance can vary based on various factors like the specific implementation of the function in the Python interpreter, the hardware it’s running on, etc.

[For most practical purposes, the time complexity of `str.replace()` can be considered linear, i.e., O(n), where ‘n’ is the length of the string](https://www.geeksforgeeks.org/python-replace-multiple-characters-at-once/)[3](https://www.geeksforgeeks.org/python-replace-multiple-characters-at-once/)[4](https://stackoverflow.com/questions/47209406/what-is-the-time-complexity-or-big-o-notation-for-str-replace-built-in-funct). [However, for large strings and numerous replacements, the time complexity could potentially be quadratic](https://stackoverflow.com/questions/66163149/does-str-replace-have-a-time-complexity-on2)[1](https://stackoverflow.com/questions/66163149/does-str-replace-have-a-time-complexity-on2)[2](https://stackoom.com/en/question/4Tc3Z).

 

​              



## Best Complexity

Time Complexity: O(n)

Space Complexity: O(n)