# 707. Design Linked List / 设计链表

leetcode: https://leetcode.com/problems/design-linked-list/description/

力扣： https://leetcode.cn/problems/design-linked-list/description/

## Solution: Single Linked List / 单链表

This problem is solved using a single linked list with a dummy head node. the question is not too hard and mainly tests on the design and manipulation of data structures.

One important detail is to clarify the relationship between the index and the dummy head node during traversal. you should consider whether to start traversing from the dummy head itself or from the node after the dummy head.

本题使用单链表加虚拟头节点设计，题目难度并不高，主要考验对于数据结构的设计和操作，需要注意的是在遍历链表时index和虚拟头节点的关系，应考虑到底是从虚拟头节点开始遍历还是虚拟头节点的下一个节点开始遍历

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

Java(didn't use dummy node / 未使用虚拟头节点)

```java
class MyLinkedList {
    class myListNode{
        int val;
        myListNode next;
        myListNode(int val){
            this.val = val;
        }
    }

    private int size;
    private myListNode head;
    // Used tail in this one to make addAtTail and get methods easier
    // but be aware that every time you modify your linked list, you always have to 
    // maintain your tail
    private myListNode tail;

    public MyLinkedList() { // didn't use dummyhead here
        this.size = 0;
    }
  
    public int get(int index) {
        if (index < 0 || index >= size) return -1;
        if (index == 0) return head.val;
        if (index == size - 1) return tail.val;

        myListNode curr = head;
        for (int i = 0; i < index; i++){
            curr = curr.next;
        }

        return curr.val;
    }
  
    public void addAtHead(int val) {
        myListNode newhead = new myListNode(val);
        if (size == 0) {
            this.head = newhead;
            this.tail = head;
            size ++;
        } else {
            newhead.next = head;
            head = newhead;
            size ++;
        }  
    }
  
    public void addAtTail(int val) {
        myListNode newTail = new myListNode(val);
        if (size == 0) {
            this.head = newTail;
            this.tail = head;
            size ++;
        } else {
            tail.next = newTail;
            tail = newTail;
            size ++;
        }  
    }
  
    public void addAtIndex(int index, int val) {
        if (index > size) return;
        if (index == 0){
            addAtHead(val);
            return;
        }
        if (index == size) {
            addAtTail(val);
            return;
        }
        myListNode curr = head;
        for (int i = 1; i < index; i++) {
            curr = curr.next;
        }

        myListNode temp = new myListNode(val);
        temp.next = curr.next;
        curr.next = temp;
        size++;

    }
  
    public void deleteAtIndex(int index) { //maintain your hea and tail
        if (index < 0 || index >= this.size) return;
        if (index == 0) {
            head = head.next;
            size --;
            if (size == 0) tail = null;
            return;
        }

        myListNode curr = head;

        for (int i = 1; i < index; i++){
            curr = curr.next;
        }
        curr.next = curr.next.next;
        size --;

        if (index == size) tail = curr;
    }
}

/**
 * Your MyLinkedList object will be instantiated and called as such:
 * MyLinkedList obj = new MyLinkedList();
 * int param_1 = obj.get(index);
 * obj.addAtHead(val);
 * obj.addAtTail(val);
 * obj.addAtIndex(index,val);
 * obj.deleteAtIndex(index);
 */
```
