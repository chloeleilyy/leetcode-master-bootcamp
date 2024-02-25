# 977

# Problem

Given an integer array `nums` sorted in **non-decreasing** order, return *an array of **the squares of each number** sorted in non-decreasing order*.

 

**Example 1:**

```
Input: nums = [-4,-1,0,3,10]
Output: [0,1,9,16,100]
Explanation: After squaring, the array becomes [16,1,0,9,100].
After sorting, it becomes [0,1,9,16,100].
```

**Example 2:**

```
Input: nums = [-7,-3,2,3,11]
Output: [4,9,9,49,121]
```

 

**Constraints:**

- `1 <= nums.length <= 10^4`
- `-10^4 <= nums[i] <= 10^4`
- `nums` is sorted in **non-decreasing** order.

 

**Follow up:** Squaring each element and sorting the new array is very trivial, could you find an `O(n)` solution using a different approach?



## Classification & Discussion





****

# Solution

![img](./images/day2.assets/977.%E6%9C%89%E5%BA%8F%E6%95%B0%E7%BB%84%E7%9A%84%E5%B9%B3%E6%96%B9.gif)



## Important details





## Code 双指针

- 写法1

```python
class Solution:
    def sortedSquares(self, nums: List[int]) -> List[int]:
        l, i = len(nums), len(nums) - 1
        left, right = 0, l - 1
        square_list = [0] * l
        while left <= right:
            if nums[left] ** 2 > nums[right] ** 2:
                square_list[i] = nums[left] ** 2
                left += 1
            else:
                square_list[i] = nums[right] ** 2
                right -= 1
            i -= 1
        return square_list

```

- 写法2

```python
# add another list.
class Solution:
    def sortedSquares(self, nums: List[int]) -> List[int]:
        square_list = []
        left, right = 0, len(nums) - 1
    
        while left <= right:
            left_val, right_val = abs(nums[left]), abs(nums[right])
            if left_val > right_val:
                square_list.append(left_val ** 2)
                left += 1
            else:
                square_list.append(right_val ** 2)
                right -= 1
        square_list.reverse()
        return square_list

# time: O(n)
# space: O(1)
```



## Code 先平方后排序

```python
class Solution:
    def sortedSquares(self, nums: List[int]) -> List[int]:
        for i in range(len(nums)):
            nums[i] = nums[i] ** 2
        nums.sort()
        return nums
# time: in average O(nlogn), python timesort
# space: O(n)
```



## Code 暴力排序法+列表推导法

```python
class Solution:
    def sortedSquares(self, nums: List[int]) -> List[int]:
        return sorted(x*x for x in nums)
# time: O(nlogn)
# space: O(n)
```

Time:

这段代码的算法复杂度主要由两部分组成：生成平方数列表和对这个列表进行排序。

1. **生成平方数列表**：这一步通过列表推导完成，对于输入列表`nums`中的每个元素，计算其平方。如果列表长度为`n`，这一步的时间复杂度是\(O(n)\)，因为它需要遍历整个列表一次。

2. **排序**：排序操作的时间复杂度依赖于Python中`sorted()`函数的实现。Python使用的是Timsort算法，这是一种结合了归并排序和插入排序的算法。对于平均情况和最坏情况，Timsort的时间复杂度都是\(O(n log n)\)。

综上所述，整个函数的时间复杂度是由第二步的排序操作决定的，即\(O(n log n)\)。尽管生成平方数列表也需要时间，但相比于排序操作，其复杂度较低，在整体复杂度分析中被排序操作的\(O(n log n)\)所主导。因此，这段代码的总体算法复杂度是\(O(n log n)\)。

Space:

代码中的空间复杂度主要由两个因素决定：生成平方数的列表推导以及`sorted()`函数的内部实现。

1. **列表推导**：在执行`sorted(x*x for x in nums)`时，列表推导会首先生成一个包含所有`nums`元素平方的新列表。这个操作的空间复杂度是 \(O(n)\)，因为它需要存储`n`个元素的平方值，其中`n`是输入列表`nums`的长度。

2. **排序操作**：`sorted()`函数返回一个新的列表，这意味着原列表被复制了一份进行排序。因此，排序过程中至少需要额外的\(O(n)\)空间来存储这个副本。然而，Timsort（Python排序算法的基础）的空间复杂度最坏情况下为 \(O(n)\)，这是因为它在合并过程中可能需要与原列表等大的额外空间。

综合上述两点，整个函数的空间复杂度是 \(O(n)\)。这包括了存储平方数列表和排序过程中可能需要的额外空间。尽管这个分析基于Timsort算法的特性，但实际的空间使用情况还可能受到Python解释器实现的具体细节影响。

## Best Complexity

Time Complexity: `O(n)`

Space Complexity: `O(1)`



# 209

# Problem

Given an array of positive integers `nums` and a positive integer `target`, return *the **minimal length** of a* 

*subarray* whose sum is greater than or equal to* `target`. If there is no such subarray, return `0` instead.

**Example 1:**

```
Input: target = 7, nums = [2,3,1,2,4,3]
Output: 2
Explanation: The subarray [4,3] has the minimal length under the problem constraint.
```

**Example 2:**

```
Input: target = 4, nums = [1,4,4]
Output: 1
```

**Example 3:**

```
Input: target = 11, nums = [1,1,1,1,1,1,1,1]
Output: 0
```

 

**Constraints:**

- `1 <= target <= 109`
- `1 <= nums.length <= 105`
- `1 <= nums[i] <= 104`

 

**Follow up:** If you have figured out the `O(n)` solution, try coding another solution of which the time complexity is `O(n log(n))`.



## Classification & Discussion





****

# Solution 1 sliding window

> 第二次做，滑动窗口自己做还是没思路

**滑动窗口**

- 用一个for循环做两个for循环所做的事情
- 一个for循环里面的指针一定指向的是终止位置
  - 如果指向的是起始位置，那么和暴力解法一样了
- 起始位置动态移动
  - 当发现集合里面的元素和 >= target 时，将起始位置向右➡️移动
- 有很多细节要注意

![leetcode_209](./images/day2.assets/20210312160441942.png)



## Important details





## Code

```python
class Solution:
    def minSubArrayLen(self, target: int, nums: List[int]) -> int:
        i, result = 0, float('inf')
        sum = 0
        for j in range(len(nums)):
            sum += nums[j]
            while sum >= target:
                sub_len = j - i + 1
                result = min(result, sub_len)
                # move i index
                sum -= nums[i]
                i += 1
        return result if result != float('inf') else 0

# time: O(n)
# space: O(1)
```

不要以为for里放一个while就以为是O(n^2)啊， 主要是看每一个元素被操作的次数，每个元素在滑动窗后进来操作一次，出去操作一次，每个元素都是被操作两次，所以时间复杂度是 2 × n 也就是O(n)。





# Solution 2  brute force

这道题目暴力解法当然是 两个for循环，然后不断的寻找符合条件的子序列，时间复杂度很明显是O(n^2)。



## Important details

- 每次移动 i 的时候重置cur_sum = 0

```python
        for i in range(len(nums)):
            cur_sum = 0
```



## Code

```python
class Solution:
    def minSubArrayLen(self, target: int, nums: List[int]) -> int:
        l = len(nums)
        min_sublen = float('inf')

        for i in range(len(nums)):
            cur_sum = 0
            for j in range(i, len(nums)):
                cur_sum += nums[j]
                if cur_sum >= target:
                    min_sublen = min(min_sublen, j - i + 1)
                    break
        
        return min_sublen if min_sublen != float('inf') else 0

# time: O(n^2)
# space: O(1)
```





## Best Complexity

Time Complexity:  O(n)

Space Complexity:  O(1)



# 59

# Problem

Given a positive integer `n`, generate an `n x n` `matrix` filled with elements from `1` to `n2` in spiral order.

 

**Example 1:**

![img](./images/day2.assets/spiraln.jpg)

```
Input: n = 3
Output: [[1,2,3],[8,9,4],[7,6,5]]
```

**Example 2:**

```
Input: n = 1
Output: [[1]]
```

 

**Constraints:**

- `1 <= n <= 20`



## Classification & Discussion





****

# Solution 模拟

- 需要注意很多细节

- 题解

  - https://github.com/youngyangyang04/leetcode-master/blob/master/problems/0059.%E8%9E%BA%E6%97%8B%E7%9F%A9%E9%98%B5II.md

    

![img](./images/day2.assets/68747470733a2f2f636f64652d7468696e6b696e672d313235333835353039332e66696c652e6d7971636c6f75642e636f6d2f706963732f32303232303932323130323233362e706e67.png)

## Important details





## Code

```python
# 模拟
class Solution:
    def generateMatrix(self, n: int) -> List[List[int]]:
        nums =[[0] * n for _ in range(n)]
        startx, starty = 0, 0
        # 如果n是奇数的话，mid就是中间剩下的数的坐标
        loop, mid = n // 2, n // 2 
        # count 用于填充数字
        count = 1 
        
        for offset in range(1, loop + 1):
            # 从左到右，左闭右开
            last_index = n - offset
            for j in range(starty, last_index):
                nums[startx][j] = count
                count += 1
            # 从上到下
            for i in range(startx, last_index):
                nums[i][last_index] = count
                count += 1
            # 从左到右
            for j in range(last_index, starty, -1):
                nums[last_index][j] = count
                count += 1
            # 从下到上
            for i in range(last_index, startx, -1):
                nums[i][starty] = count
                count += 1
            # update start index
            startx += 1
            starty += 1

        if n % 2 == 1:
            nums[mid][mid] = count

        return nums
                
# time: O(n^2)
# space: O(1)
        
```





## Complexity

Time Complexity: O(n^2)

Space Complexity: O(1)