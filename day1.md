# 704

# Problem

Given an array of integers `nums` which is sorted in ascending order, and an integer `target`, write a function to search `target` in `nums`. If `target` exists, then return its index. Otherwise, return `-1`.

You must write an algorithm with `O(log n)` runtime complexity.

 

**Example 1:**

```
Input: nums = [-1,0,3,5,9,12], target = 9
Output: 4
Explanation: 9 exists in nums and its index is 4
```

**Example 2:**

```
Input: nums = [-1,0,3,5,9,12], target = 2
Output: -1
Explanation: 2 does not exist in nums so return -1
```

 

**Constraints:**

- `1 <= nums.length <= 10^4`
- `-10^4 < nums[i], target < 10^4`
- All the integers in `nums` are **unique**.
- `nums` is sorted in ascending order.



## Classification & Discussion

朴素二分法

**这道题目的前提是数组为有序数组**，同时题目还强调**数组中无重复元素**，因为一旦有重复元素，使用二分查找法返回的元素下标可能不是唯一的，这些都是使用二分法的前提条件，当大家看到题目描述满足如上条件的时候，可要想一想是不是可以用二分法了。



****

# Solution





## Important details

- `left + (right - left) // 2`



## Code 1

- manually binary search

```python
# binary search
# while -> 
# 1. set left and right (left inclusive, right exclusive)
# 2. get mid
# 3. compare mid_num with target

class Solution:
    def search(self, nums: List[int], target: int) -> int:
        left, right = 0, len(nums)
        while left < right:
            mid_index = left + (right - left) // 2
            mid_num = nums[mid_index]
            if target == mid_num:
                return mid_index
            elif target < mid_num:
                right = mid_index
            else:
                left = mid_index + 1
        return -1

# time: O(logN)
# space: O(1)    
```



## Code 2

- Use python lib bisect

- [bisect](../00_python/bisect.md)

```python
class Solution:
    def search(self, nums: List[int], target: int) -> int:
        index = bisect.bisect_left(nums, target)
        if index != len(nums) and nums[index] == target:
            return index
        return -1
      
# time: O(logN)
# space: O(1)
```



## Complexity

Time Complexity:  `O(logN)`

Space Complexity: `O(1)`



# 27

# Problem

Given an integer array `nums` and an integer `val`, remove all occurrences of `val` in `nums` [**in-place**](https://en.wikipedia.org/wiki/In-place_algorithm). The order of the elements may be changed. Then return *the number of elements in* `nums` *which are not equal to* `val`.

Consider the number of elements in `nums` which are not equal to `val` be `k`, to get accepted, you need to do the following things:

- Change the array `nums` such that the first `k` elements of `nums` contain the elements which are not equal to `val`. The remaining elements of `nums` are not important as well as the size of `nums`.
- Return `k`.

**Custom Judge:**

The judge will test your solution with the following code:

```
int[] nums = [...]; // Input array
int val = ...; // Value to remove
int[] expectedNums = [...]; // The expected answer with correct length.
                            // It is sorted with no values equaling val.

int k = removeElement(nums, val); // Calls your implementation

assert k == expectedNums.length;
sort(nums, 0, k); // Sort the first k elements of nums
for (int i = 0; i < actualLength; i++) {
    assert nums[i] == expectedNums[i];
}
```

If all assertions pass, then your solution will be **accepted**.

 

**Example 1:**

```
Input: nums = [3,2,2,3], val = 3
Output: 2, nums = [2,2,_,_]
Explanation: Your function should return k = 2, with the first two elements of nums being 2.
It does not matter what you leave beyond the returned k (hence they are underscores).
```

**Example 2:**

```
Input: nums = [0,1,2,2,3,0,4,2], val = 2
Output: 5, nums = [0,1,4,0,3,_,_,_]
Explanation: Your function should return k = 5, with the first five elements of nums containing 0, 0, 1, 3, and 4.
Note that the five elements can be returned in any order.
It does not matter what you leave beyond the returned k (hence they are underscores).
```

 

**Constraints:**

- `0 <= nums.length <= 100`
- `0 <= nums[i] <= 50`
- `0 <= val <= 100`



## Classification & Discussion





****



# Solution 1  快慢指针的 slow, fast

双指针法（快慢指针法）： **通过一个快指针和慢指针在一个for循环下完成两个for循环的工作。**

定义快慢指针

- 快指针：寻找新数组的元素 ，新数组就是不含有目标元素的数组
- 慢指针：指向更新 新数组下标的位置

![27.移除元素-双指针法](./day1.assets/27.%E7%A7%BB%E9%99%A4%E5%85%83%E7%B4%A0-%E5%8F%8C%E6%8C%87%E9%92%88%E6%B3%95.gif)

## Important details



## Code

- 可以理解为用slow指针记录fast指针中不是val的元素

```python
class Solution:
    def removeElement(self, nums: List[int], val: int) -> int:
        slow_index = 0
        for fast_index in range(len(nums)):
            if nums[fast_index] != val:
                nums[slow_index] = nums[fast_index]
                slow_index += 1
        return slow_index
        
```





## Complexity

Time Complexity: O(n)

Space Complexity: O(1)





# Solution 2  brute force

有的同学可能说了，多余的元素，删掉不就得了。

**要知道数组的元素在内存地址中是连续的，不能单独删除数组中的某个元素，只能覆盖。**

![27.移除元素-暴力解法](./day1.assets/27.%E7%A7%BB%E9%99%A4%E5%85%83%E7%B4%A0-%E6%9A%B4%E5%8A%9B%E8%A7%A3%E6%B3%95.gif)



## Important details

这段代码尝试在遍历列表的同时修改列表的长度，这会导致问题。问题的根源在于，当你从列表中删除元素时，后面的元素会向前移动，这会导致索引与当前遍历的位置不同步。因此，你可能会跳过一些元素，或者在尝试访问某个索引时遇到`IndexError`，因为`l`已经减少了，但是`range(l)`是在循环开始前就计算好的，所以不会动态调整。

```python
l = len(nums) 
for i in range(l):
    if nums[i] == val:
        nums.pop(i)
        l -= 1
return l
```

一个更安全且有效的方式是从后向前遍历列表，这样即使删除了当前元素，也不会影响到未遍历到的元素的索引。下面是修改后的代码示例：

```python
for i in range(len(nums) - 1, -1, -1):
    if nums[i] == val:
        nums.pop(i)
# 返回修改后的列表长度
return len(nums)
```

这种方式通过逆序遍历，确保在删除元素时不会干扰到尚未检查的元素的索引，避免了上述问题。此外，它直接返回修改后的列表长度，而不是尝试在循环中动态调整长度变量`l`。



## Code

- 在while loop 中`l` 会动态调整

```python
class Solution:
    def removeElement(self, nums: List[int], val: int) -> int:
        i, l = 0, len(nums)
        while i < l:
            if nums[i] == val:
                nums.pop(i)
                l -= 1
            else:
                i += 1
        return l
```



- 在range中从后向前遍历

```python
class Solution:
    def removeElement(self, nums: List[int], val: int) -> int:
        for i in range(len(nums) - 1, -1, -1):
            if nums[i] == val:
                nums.pop(i)
        return len(nums)
# time: O(n^2)
# space: O(1)
```

## Complexity

Time Complexity: `O(n^2)`

Space Complexity: `O(1)`





# Solution 3  相向指针法，left, right





## Important details





## Code 

- 简洁一点的解法

```python
# we want to swith left elements that are equal to val and 
# right elements that are not equal to val
class Solution:
    def removeElement(self, nums: List[int], val: int) -> int:
        left, right = 0, len(nums) - 1
        while left <= right:
            # find right elements that are not equal to val
            while right >= 0 and nums[right] == val:
                right -= 1
            # find left elements that are equal to val
            while left < len(nums) and nums[left] != val:
                left += 1
            if left <= right:
                # it's OK that only replace nums[left]
                nums[left], nums[right] = nums[right], nums[left]
                left += 1
                right -= 1
        return right + 1
                
            
```





- 第一次自己写的解法

```python
# two pointers
class Solution:
    def removeElement(self, nums: List[int], val: int) -> int:
        if len(nums) == 0:
            return 0
        left, right = 0, len(nums) - 1
        while left <= right:
            if nums[right] == val:
                right -= 1
            elif nums[left] == val:
                nums[left], nums[right] = nums[right], nums[left]
                left += 1
                right -= 1
            else:
                left += 1
        return right + 1
```





## Complexity

Time Complexity:   `O(n)`

Space Complexity:  `O(1)`