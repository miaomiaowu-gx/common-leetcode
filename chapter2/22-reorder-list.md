## 22 重排链表

给定一个单链表 L：L0→L1→…→Ln-1→Ln ，
将其重新排列后变为： L0→Ln→L1→Ln-1→L2→Ln-2→…

你不能只是单纯的改变节点内部的值，而是需要实际的进行节点交换。

```
示例 1:
给定链表 1->2->3->4, 重新排列为 1->4->2->3.

示例 2:
给定链表 1->2->3->4->5, 重新排列为 1->5->2->4->3.
```


[143. 重排链表](https://leetcode-cn.com/problems/reorder-list/)



### 寻找链表中点 + 链表逆序 + 合并链表


注意到目标链表即为将原链表的左半端和反转后的右半端合并后的结果。这样任务即可划分为三步：

1. 找到原链表的中点（参考「876. 链表的中间结点」）。

    * 可以使用快慢指针来 O(N) 地找到链表的中间节点。

2. 将原链表的右半端反转（参考「206. 反转链表」）。

    * 可以使用迭代法实现链表的反转。

3. 将原链表的两端合并。

因为两链表长度相差不超过 1，因此直接合并即可。

```java

class Solution {
    public void reorderList(ListNode head) {
        if(head==null) return;
        ListNode mid = middleNode(head);
        ListNode midrev= reverseList(mid.next);
        //将链表从中部断开
        mid.next = null;
        mergeList(head, midrev);
    }

    //偶数，找前一个节点
    public ListNode middleNode(ListNode head){
        ListNode slow = head, fast = head;
        while (fast!=null && fast.next!=null && fast.next.next!=null){
            fast = fast.next.next;
            slow = slow.next;
        }
        return slow;
    }

    public ListNode reverseList(ListNode head){
        ListNode pre = null, cur = head;
        while (cur!=null){
            ListNode t = cur.next;
            cur.next = pre;
            pre = cur;
            cur = t;
        }
        return pre;
    }

    public void mergeList(ListNode l1, ListNode l2){
        ListNode t1;
        ListNode t2;
        //l1.len > l2.len
        while (l1!=null && l2!=null){
            t1 = l1.next;
            t2 = l2.next;

            l1.next = l2;
            l1 = t1;

            l2.next = l1;
            l2 = t2;
        }
    }
}
```



### 线性表