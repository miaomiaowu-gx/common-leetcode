## 16 旋转链表

给定一个链表，旋转链表，将链表每个节点向右移动 k 个位置，其中 k 是非负数。

示例 1:

```
输入: 1->2->3->4->5->NULL, k = 2
输出: 4->5->1->2->3->NULL
解释:
向右旋转 1 步: 5->1->2->3->4->NULL
向右旋转 2 步: 4->5->1->2->3->NULL
```

示例 2:

```
输入: 0->1->2->NULL, k = 4
输出: 2->0->1->NULL
解释:
向右旋转 1 步: 2->0->1->NULL
向右旋转 2 步: 1->2->0->NULL
向右旋转 3 步: 0->1->2->NULL
向右旋转 4 步: 2->0->1->NULL
```

[61. 旋转链表](https://leetcode-cn.com/problems/rotate-list/)


### 直接法


思路：先将链表闭合成环，找到相应的位置断开这个环，确定新的链表头和链表尾。

1. 找到旧的尾部并将其与链表头相连 old_tail.next = head，整个链表闭合成环，同时计算出链表的长度 n。

2. 找到新的尾部，第 (n - k % n - 1) 个节点 ，新的链表头是第 (n - k % n) 个节点。

3. 断开环 `new_tail.next = None`，并返回新的链表头 new_head。


```java
class Solution {
    public ListNode rotateRight(ListNode head, int k) {
        if(head==null || head.next==null) return head;
        int len = 0;
        ListNode newHead = null, curr=head;
        while (curr!=null && curr.next!=null){
            len++;
            curr = curr.next;
        }
        len++; //最后一个节点
        curr.next = head; //连接成环
        curr = head;
        for(int i=0; i<len- k%len -1;i++){
            curr = curr.next;
        }
        newHead = curr.next;
        curr.next = null;
        return newHead;
    }
}
```



复杂度分析

* 时间复杂度：O(N)，其中 N 是链表中的元素个数

* 空间复杂度：O(1)，因为只需要常数的空间






