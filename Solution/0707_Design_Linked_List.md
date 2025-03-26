# 707. Design Linked List / 设计链表

leetcode: https://leetcode.com/problems/design-linked-list/description/

力扣： https://leetcode.cn/problems/design-linked-list/description/

## Solution: Single Linked List / 单链表

This problem is solved using a single linked list with a dummy head node. the question is not too hard and mainly tests on the design and manipulation of data structures.

One important detail is to clarify the relationship between the index and the dummy head node during traversal. you should consider whether to start traversing from the dummy head itself or from the node after the dummy head.

本题使用单链表加虚拟头节点设计，题目难度并不高，主要考验对于数据结构的设计和操作，需要注意的是在遍历链表时index和虚拟头节点的关系，应考虑到底是从虚拟头节点开始遍历还是虚拟头节点的下一个节点开始遍历

Java

```

```

python

```python
class list_node:
    def __init__(self, val = 0, next = None):
        self.val = val
        self.next = next

class MyLinkedList:

    def __init__(self):
        self.dummyhead = list_node()
        self.size = 0

    def get(self, index: int) -> int:
        if index < 0 or index >= self.size:
            return -1
    
        current = self.dummyhead.next
        for i in range(index):
            current = current.next
        return current.val

    def addAtHead(self, val: int) -> None:
        temp = list_node(val, self.dummyhead.next)
        self.dummyhead.next = temp
        self.size += 1
    
    def addAtTail(self, val: int) -> None:
        current = self.dummyhead
        while current.next:
            current = current.next
    
        current.next = list_node(val)
        self.size += 1

    def addAtIndex(self, index: int, val: int) -> None:
        if index < 0 or index > self.size:
            return
    
        if index == self.size:
            self.addAtTail(val)
            return
    
        current = self.dummyhead
        for i in range(index):
            current = current.next
    
        current.next = list_node(val, current.next)
        self.size += 1 

    def deleteAtIndex(self, index: int) -> None:
        if index < 0 or index >= self.size:
            return
    
        if index == 0:
            self.dummyhead.next = self.dummyhead.next.next
            self.size -= 1
            return
    
        current = self.dummyhead
        for i in range(index):
            current = current.next
    
        current.next = current.next.next
        self.size -= 1
    


# Your MyLinkedList object will be instantiated and called as such:
# obj = MyLinkedList()
# param_1 = obj.get(index)
# obj.addAtHead(val)
# obj.addAtTail(val)
# obj.addAtIndex(index,val)
# obj.deleteAtIndex(index)
```
