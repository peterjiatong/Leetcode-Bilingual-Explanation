# 19. Remove Nth Node From End of List / 删除链表的倒数第 N 个结点

leetcode: https://leetcode.com/problems/remove-nth-node-from-end-of-list

力扣：https://leetcode.cn/problems/remove-nth-node-from-end-of-list

## Solution: Two Pointers / 双指针

We use two pointers, the right pointer is responsible for detecting when we've reached the end of the list, and the left pointer marks the node before the one that needs to be removed. We first move the right pointer `n` steps forward. Then, we move both pointers simultaneously until the right pointer's next node is `null`. At that point, the node after the left pointer is the one to be deleted. This algorithm has a time complexity of `O(n)`.

Please note that if the right pointer is already `null` after moving `n` steps, it means the node to be deleted is the first node. In this case, we can simply return `head.next`.

使用左右两个指针，右指针负责判断出界，左指针负责标记需要删除的节点的前一个节点。首先先让右指针向前走n步，之后同时移动左右指针，当右指针的下一个节点为空节点时，左指针的下一个节点即为需要删除的节点，此算法时间复杂度为 `O(n)`

需要注意的是，若右指针向前走n步后已经是空节点，说明需要删除第一个节点，直接返回`head.next`即可

Java


python

```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution(object):
    def removeNthFromEnd(self, head, n):
        """
        :type head: Optional[ListNode]
        :type n: int
        :rtype: Optional[ListNode]
        """
        # Corner case
        if not head.next:
            return None
  
        right_node = head
        left_node = head

	# Move right_node n step forward
        for i in range(n):
            right_node = right_node.next

	# Edge case, if n == sz
        if right_node is None:
            return head.next

        while right_node.next:
            right_node = right_node.next
            left_node = left_node.next
  
        left_node.next = left_node.next.next
        return head
```
