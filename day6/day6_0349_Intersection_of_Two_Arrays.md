# Problem

Given two integer arrays `nums1` and `nums2`, return *an array of their intersection*. Each element in the result must be **unique** and you may return the result in **any order**.

 

**Example 1:**

```
Input: nums1 = [1,2,2,1], nums2 = [2,2]
Output: [2]
```

**Example 2:**

```
Input: nums1 = [4,9,5], nums2 = [9,4,9,8,4]
Output: [9,4]
Explanation: [4,9] is also accepted.
```

 

**Constraints:**

- `1 <= nums1.length, nums2.length <= 1000`
- `0 <= nums1[i], nums2[i] <= 1000`



## Classification & Discussion





****

# Solution

- 使用python set

### ==Step==

1. 
2. 





## Important details





## Code

```python
class Solution:
    def intersection(self, nums1: List[int], nums2: List[int]) -> List[int]:
        # space: O(m) time: O(m)
        set1 = {nums1}
        set2 = set()
        # space: O(k) time: O(n)
        for num in nums2:
            if num in set1:
                set2.add(num)
        # time: O(k), space: O(k)
        return list(set2)

# time: O(m + n + k)
# space: O(m + k)
```



## Code

```python
class Solution:
    def intersection(self, nums1: List[int], nums2: List[int]) -> List[int]:
        set1 = {x for x in nums1}
        set2 = {x for x in nums2}

        # O(min(m,n)) 
        return list(set1 & set2)

# time: O(m + n)
# space: O(m + n + k)
```



## Code

```python
class Solution:
    def intersection(self, nums1: List[int], nums2: List[int]) -> List[int]:
        # set comprehensions
        intersection_set = { x for x in nums1 if x in nums2}
        return intersection_set

# time: O(mn), m is nums1 length, n is nums2 length
# space: O(k), k = the length of intersection
```

```python
class Solution:
    def intersection(self, nums1: List[int], nums2: List[int]) -> List[int]:
        return list(set(nums1) & set(nums2))
```



## Best Complexity

Time Complexity: O(m + n + k)

Space Complexity: O(m + k)

 