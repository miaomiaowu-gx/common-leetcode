## 14 删除链表的倒数第N个节点


给定一个链表，删除链表的倒数第 n 个节点，并且返回链表的头结点。

示例：

```
给定一个链表: 1->2->3->4->5, 和 n = 2.
当删除了倒数第二个节点后，链表变为 1->2->3->5.
```

说明：给定的 n 保证是有效的。

进阶：你能尝试使用一趟扫描实现吗？

[19. 删除链表的倒数第N个节点](https://leetcode-cn.com/problems/remove-nth-node-from-end-of-list/)



### 一次遍历(双指针)

```java
class Solution {
    public ListNode removeNthFromEnd(ListNode head, int n) {
        ListNode newHead = new ListNode(-1);
        newHead.next = head;

        ListNode fast = newHead, slow = newHead;
        while (n-- >= 0 && fast!=null){
            fast = fast.next;
        }
        while (fast!=null){ 
            //由于此处判断为 fast!=null，上一步先走了n+1步
            //若判断为 fast!=null&&fast.next!=null，则只需走n步
            fast = fast.next;
            slow = slow.next;
        }
        if(slow!=null && slow.next!=null){
            slow.next = slow.next.next;
        }
        return newHead.next;
    }
}
```


### 计算链表长度

```java
class Solution {
    public ListNode removeNthFromEnd(ListNode head, int n) {
        ListNode dummy = new ListNode(0, head);
        int length = getLength(head);
        ListNode cur = dummy;
        for (int i = 1; i < length - n + 1; ++i) {
            cur = cur.next;
        }
        cur.next = cur.next.next;
        return dummy.next;
    }

    public int getLength(ListNode head) {
        int length = 0;
        while (head != null) {
            ++length;
            head = head.next;
        }
        return length;
    }
}
```
