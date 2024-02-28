# Problem

Given a linked list, swap every two adjacent nodes and return its head. You must solve the problem without modifying the values in the list's nodes (i.e., only nodes themselves may be changed.)

 

**Example 1:**

![img](./images/day4_0024_Swap_Nodes_in_Pairs.assets/swap_ex1.jpg)

```
Input: head = [1,2,3,4]
Output: [2,1,4,3]
```

**Example 2:**

```
Input: head = []
Output: []
```

**Example 3:**

```
Input: head = [1]
Output: [1]
```

 

**Constraints:**

- The number of nodes in the list is in the range `[0, 100]`.
- `0 <= Node.val <= 100`



## Classification & Discussion

这道题很考验链表操作



****

# Solution

- 代码随想录视频题解

https://www.bilibili.com/video/BV1YT411g7br/?vd_source=3c420743568231df80019ab65f2b0404



### ==Step==

1. 考虑到需要对链表头节点操作，所以要使用dummy head
2. 需要交换节点时实际就是操作链表指针
3. 当可能会丢失节点的时候就需要用额外的指针保存，比如本题中的temp





## Important details

- 注意节点是奇数个和偶数个的情况
- 指针赋值顺序



## Code

本题可以只保存一个temp节点, 或者保存两个temp节点

- 保存一个temp节点

![image-20240228000809821](./images/day4_0024_Swap_Nodes_in_Pairs.assets/image-20240228000809821.png)

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def swapPairs(self, head: Optional[ListNode]) -> Optional[ListNode]:
        dummy_head = ListNode(next=head)
        current = dummy_head
        while current.next != None and current.next.next != None:
            temp = current.next
            current.next = current.next.next
            temp.next = temp.next.next
            current.next.next = temp
            # move current pointer
            current = current.next.next
        return dummy_head.next
    
```



- 保存两个temp节点 【code from 代码随想录】

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next

class Solution:
    def swapPairs(self, head: ListNode) -> ListNode:
        dummy_head = ListNode(next=head)
        current = dummy_head
        
        # 必须有cur的下一个和下下个才能交换，否则说明已经交换结束了
        while current.next and current.next.next:
            temp = current.next # 防止节点修改
            temp1 = current.next.next.next
            
            current.next = current.next.next
            current.next.next = temp
            temp.next = temp1
            current = current.next.next
        return dummy_head.next
```





## Complexity

Time Complexity: O(n)

Space Complexity: O(1)