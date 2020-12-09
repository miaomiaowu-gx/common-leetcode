## 13 两数相加/链表求和

给出两个 非空 的链表用来表示两个非负的整数。其中，它们各自的位数是按照 逆序 的方式存储的，并且它们的每个节点只能存储 一位 数字。

如果，将这两个数相加起来，则会返回一个新的链表来表示它们的和。

您可以假设除了数字 0 之外，这两个数都不会以 0 开头。

示例：

```
输入：(2 -> 4 -> 3) + (5 -> 6 -> 4)
输出：7 -> 0 -> 8
原因：342 + 465 = 807
```

[2. 两数相加](https://leetcode-cn.com/problems/add-two-numbers/)


### 模拟运算过程

```java
class Solution {
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        ListNode head = new ListNode(-1), cur = head;
        int flag = 0; //是否有进位
        ListNode p1 = l1, p2 = l2;
        while (p1!=null || p2!=null){
            int val1 = p1==null? 0 : p1.val;
            int val2 = p2==null? 0 : p2.val;
            int val = val1 + val2 + flag;
            //连接新节点，并移动到尾部
            cur.next = new ListNode(val % 10);
            cur = cur.next;
            flag = val /10;
            //遍历两个链表！
            p1 = p1==null? null : p1.next;
            p2 = p2==null? null : p2.next;
        }
        //判断最高位是否有进位！
        if(flag!=0){
            ListNode t = new ListNode(flag);
            cur.next = t;
        }
        return head.next;
    }
}
```

复杂度分析

* 时间复杂度：O(max(m,n))，其中 m,n 为两个链表的长度。要遍历两个链表的全部位置，而处理每个位置只需要 O(1) 的时间。

* 空间复杂度：O(max(m,n))。结果链表的长度最多为较长链表的长度 +1。



## 进阶

思考一下，假设这些数位是正向存放的，又该如何解决呢?

示例：

```
输入：(6 -> 1 -> 7) + (2 -> 9 -> 5)，即617 + 295
输出：9 -> 1 -> 2，即912
```

