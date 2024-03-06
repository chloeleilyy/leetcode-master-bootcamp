# Problem

Given two strings `ransomNote` and `magazine`, return `true` *if* `ransomNote` *can be constructed by using the letters from* `magazine` *and* `false` *otherwise*.

Each letter in `magazine` can only be used once in `ransomNote`.

 

**Example 1:**

```
Input: ransomNote = "a", magazine = "b"
Output: false
```

**Example 2:**

```
Input: ransomNote = "aa", magazine = "ab"
Output: false
```

**Example 3:**

```
Input: ransomNote = "aa", magazine = "aab"
Output: true
```

 

**Constraints:**

- `1 <= ransomNote.length, magazine.length <= 105`
- `ransomNote` and `magazine` consist of lowercase English letters.



## Classification & Discussion





****

# Solution



### ==Step==

1. 
2. 





## Important details





## Code use dict 

- 和 242 题基本一致
- [day6_0242_Valid_Anagram](day6_0242_Valid_Anagram.md)

```python
from collections import defaultdict

class Solution:
    def canConstruct(self, ransomNote: str, magazine: str) -> bool:
        record_magazine = defaultdict(int)
        for c in magazine:
            record_magazine[c] += 1
        for c in ransomNote:
            if record_magazine[c] == 0:
                return False
            record_magazine[c] -= 1
        return True

# time: O(m + n)
# space: O(m)

```



## Code use Counter

```python
from collections import Counter

class Solution:
    def canConstruct(self, ransomNote: str, magazine: str) -> bool:
        return not Counter(ransomNote) - Counter(magazine)
```

1. `Counter(ransomNote)`和`Counter(magazine)`分别创建两个计数器对象，这两个对象计算`ransomNote`和`magazine`中每个字符的出现次数。
2. 然后，它通过从`ransomNote`的计数器中减去`magazine`的计数器来确定是否所有`ransomNote`中的字符都以足够的数量存在于`magazine`中。在`Counter`对象中，减法操作会移除结果中小于等于零的项。如果`ransomNote`中的某个字符在`magazine`中不存在或数量不足，结果中就会包含这个字符。
3. 如果`ransomNote`能够由`magazine`构建，那么减法的结果应该是一个空的`Counter`对象，表示没有任何字符缺失或数量不足。因此，`not Counter(ransomNote) - Counter(magazine)`的结果会是`True`，表示可以构造赎金信。否则，如果减法结果非空，表示无法构造，函数返回`False`。

**时间复杂度**：O(m + n)

1. **构造`Counter`对象：** 对于`ransomNote`和`magazine`字符串，构造各自的`Counter`对象的时间复杂度是O(N)和O(M)，其中N和M分别是这两个字符串的长度。这是因为`Counter`需要遍历整个字符串来计数每个字符的出现次数。
2. **执行`Counter`对象之间的减法操作：** 减法操作的时间复杂度取决于两个`Counter`对象中元素的数量。在最坏的情况下，即`ransomNote`和`magazine`中的每个字符都不同，这将与字符串的长度成正比。然而，在实际情况中，字符的种类是有限的（比如ASCII字符只有128个），所以这个操作的时间复杂度通常可以视为O(1)或O(K)，其中K是不同字符的数量，这是一个相对较小的常数。但从理论上讲，考虑到字符可能完全不同，这个步骤的时间复杂度应该被视为O(N+M)，因为减法操作涉及到遍历两个`Counter`对象中的所有元素。

**空间复杂度**：O(m +n )

这段代码的空间复杂度同样受到两个主要因素的影响：构造`Counter`对象以及执行`Counter`对象之间的减法操作。以下是对空间复杂度的分析：

1. **构造`Counter`对象：** 对于`ransomNote`和`magazine`字符串，构造各自的`Counter`对象需要存储每个唯一字符及其计数。在最坏的情况下，如果所有字符都是唯一的，那么空间复杂度将与字符串的长度成正比。然而，在实际应用中，字符的种类通常是有限的（例如，ASCII字符集中只有128个不同的字符），这意味着所需的空间主要取决于不同字符的数量，而不是字符串的总长度。因此，这部分的空间复杂度可以视为O(K)，其中K是字符串中不同字符的最大数量。

2. **执行`Counter`对象之间的减法操作：** 减法操作本身不会显著增加空间复杂度，因为它主要在现有的`Counter`对象上进行，并产生一个新的`Counter`对象。这个新的`Counter`对象的大小取决于`ransomNote`中不同字符的数量，最坏情况下等于`ransomNote`中的字符种类数量。

综上所述，整个函数的空间复杂度主要取决于输入字符串中不同字符的数量。在考虑到字符集有限的前提下，空间复杂度可以认为是O(K)，其中K是`ransomNote`和`magazine`中出现的不同字符的最大数量。这通常是一个相对较小的常数，特别是当比较的字符串是基于常见字符集（如ASCII）时。然而，从理论上讲，如果考虑到极端情况下字符串中所有字符都不同，空间复杂度可以达到O(N+M)，其中N和M分别是`ransomNote`和`magazine`的长度。但在实际应用中，这种情况很少见，特别是对于基于标准字符集的文本数据。

## Best Complexity

Time Complexity: O(m + n)

Space Complexity: O(m)