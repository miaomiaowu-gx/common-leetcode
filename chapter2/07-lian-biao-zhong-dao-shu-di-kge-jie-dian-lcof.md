## 8 链表中倒数第k个节点


输入一个链表，输出该链表中倒数第 k 个节点。为了符合大多数人的习惯，本题从 1 开始计数，即链表的尾节点是倒数第 1 个节点。例如，一个链表有 6 个节点，从头节点开始，它们的值依次是 1、2、3、4、5、6。这个链表的倒数第 3 个节点是值为 4 的节点。

 
示例：

```
给定一个链表: 1->2->3->4->5, 和 k = 2.
返回链表 4->5
```



[剑指 Offer 22. 链表中倒数第k个节点](https://leetcode-cn.com/problems/lian-biao-zhong-dao-shu-di-kge-jie-dian-lcof/)


### 快慢指针

定义两个指针，指针 1 先走 k-1 步，然后指针 2 和指针 1 同时前进，当指针 1 指向链表最后一个元素时，指针 2 即为所求。

```java
class Solution {
    public ListNode getKthFromEnd(ListNode head, int k) {
        if(head==null || k<1) return head;
        ListNode front = head, back = head;
        while(--k>0 && back!=null){
            back = back.next;
        }
        while (back!=null && back.next!=null){
            front = front.next;
            back = back.next;
        }
        return front;
    }
}
```

