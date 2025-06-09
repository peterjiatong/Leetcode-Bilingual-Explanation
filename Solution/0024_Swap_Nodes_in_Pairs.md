# 24. Swap Nodes in Pairs / 两两交换链表中的节点

leetcode: https://leetcode.com/problems/swap-nodes-in-pairs/description/

力扣：https://leetcode.cn/problems/swap-nodes-in-pairs/description/

## Solution 1: Recursion / 递归法

The problem requires swapping every two adjacent nodes in a linked list. I chose to use a recursive approach that first reaches the last node that doesn't need to be swapped (either a single final node or a null node), and then swaps nodes in reverse order on the way back up the recursion. This algorithm has a time complexity of `O(n)`. Since recursion uses the system stack space, so the space complexity is also `O(n)`.

题目要求两两交换链表中的节点，我选择使用递归先找到最后一个不需要交换的节点（最后一个单独的节点或者是为空的节点），之前从前往后交换节点顺序，此算法时间复杂度为 `O(n)`，由于递归占用系统栈，所以空间复杂度也为 `O(n)`

Java

Python

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def swapPairs(self, head: Optional[ListNode]) -> Optional[ListNode]:
        # Base case
        if head is None or head.next is None:
            return head

        newhead = self.swapPairs(head.next.next)
        # save head.next since we are going to link head to newhead
        headToReturn = head.next
        head.next.next = head
        head.next = newhead
        return headToReturn

```

## Solution 2: Iterative / 迭代法
