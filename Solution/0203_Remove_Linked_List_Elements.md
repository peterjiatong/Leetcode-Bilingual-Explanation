# Remove Linked List Elements / 移除链表元素

Leetcode: https://leetcode.com/problems/remove-linked-list-elements/description/

中文力扣：https://leetcode.cn/problems/remove-linked-list-elements/description/

## Solution 1: Traverse Linked List / 遍历链表

Before traversing the linked list, the head node should be preprocessed to ensure that `head != val `and `head` is not a null node

This problem can also be solved using a dummy head node, with a similar approach to this solution

在遍历链表开始前，应该先对头节点进行预处理，确定 `head != val`且 `head`不为空节点

本题还可以使用虚拟头节点，解题思路与此解法类似

Java

```java
class Solution {
    public ListNode removeElements(ListNode head, int val) {
        while (head != null && head.val == val){
            head = head.next;
        }

        if (head == null) return head;

        ListNode curr = head;
        while(curr != null && curr.next != null){
            if (curr.next.val == val){
                curr.next = curr.next.next;
            } else {
                curr = curr.next;
            }
        }

        return head;
    }
}
```

python

```python
class Solution:
    def removeElements(self, head: Optional[ListNode], val: int) -> Optional[ListNode]:
        while (head and head.val == val):
            head = head.next

        if not head:
            return head

        curr = head
        while curr and curr.next:
            while curr.next and curr.next.val == val:
                curr.next = curr.next.next
            curr = curr.next

        return head
```

## Solution 2: Recursion / 递归

The recursive approach for this problem is to first locate the last node (null node), then recursively traverse the linked list from backard. 

Whenever the current node's value equals `val`, return the next node of current node, which effectively skipping the current node

本题使用递归的解题思路是先找到最后一个节点（空节点），之后从后往前递归遍历链表，每当当前节点的值等于`val`，向上返值时返回当前节点的下一个节点（跳过当前节点）

Java

```java
class Solution {
    public ListNode removeElements(ListNode head, int val) {
        // 寻找最后一个节点
        if (head == null) return head;

        head.next = removeElements(head.next, val);
        if (head.val == val) return head.next; // 跳过当前节点
        return head;
    }
}
```

Python

```python
class Solution:
    def removeElements(self, head: Optional[ListNode], val: int) -> Optional[ListNode]:
        if not head:
            return head

        head.next = self.removeElements(head.next, val)
        if (head.val == val):
            return head.next
        return head
```
