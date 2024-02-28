# Problem

Given the `head` of a linked list, remove the `nth` node from the end of the list and return its head.

 

**Example 1:**

![img](./images/day4_0019_Remove_Nth_Node_From_End_of_List.assets/remove_ex1.jpg)

```
Input: head = [1,2,3,4,5], n = 2
Output: [1,2,3,5]
```

**Example 2:**

```
Input: head = [1], n = 1
Output: []
```

**Example 3:**

```
Input: head = [1,2], n = 1
Output: [1]
```

 

**Constraints:**

- The number of nodes in the list is `sz`.
- `1 <= sz <= 30`
- `0 <= Node.val <= 100`
- `1 <= n <= sz`

 

**Follow up:** Could you do this in one pass?



## Classification & Discussion





****

# Solution

- 双指针解法要比一般解法更简洁和直接，写代码也更快

![image-20240228010048076](./images/day4_0019_Remove_Nth_Node_From_End_of_List.assets/image-20240228010048076.png)

### ==Step==

- 因为有可能删除的是头节点，所以需要dummy_head
- 找到要删除的节点位置即可
- 这种找位置的题目可以使用双指针定位



## Important details





## Code

- 一般解法

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def removeNthFromEnd(self, head: Optional[ListNode], n: int) -> Optional[ListNode]:
        dummy_head = ListNode(next=head)
        current = dummy_head
        list_len = 0
        while current.next != None:
            current = current.next
            list_len += 1
        # 
        step = list_len - n
        current = dummy_head
        for i in range(step):
            current = current.next
        # delete the node
        current.next = current.next.next
        return dummy_head.next

# time: O(n)
# space: O(1)
```

- 双指针解法

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def removeNthFromEnd(self, head: Optional[ListNode], n: int) -> Optional[ListNode]:
        dummy_head = ListNode(next=head)
        fast, slow = dummy_head, dummy_head
        for i in range(n):
            fast = fast.next
        while fast.next != None:
            fast = fast.next
            slow = slow.next
        slow.next = slow.next.next
        return dummy_head.next
            
# time: O(n)
# space: O(1)
```





## Complexity

Time Complexity: O(n)

Space Complexity: O(1)