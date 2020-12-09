## 11 判断链表是否相交

编写一个程序，找到两个单链表相交的起始节点。不相交返回 null。

```
输入：intersectVal = 8, listA = [4,1,8,4,5], listB = [5,0,1,8,4,5], skipA = 2, skipB = 3
输出：Reference of the node with value = 8
输入解释：相交节点的值为 8 （注意，如果两个链表相交则不能为 0）。从各自的表头开始算起，链表 A 为 [4,1,8,4,5]，链表 B 为 [5,0,1,8,4,5]。在 A 中，相交节点前有 2 个节点；在 B 中，相交节点前有 3 个节点。
```

[160. 相交链表](https://leetcode-cn.com/problems/intersection-of-two-linked-lists/)

### 双指针法

1. 创建两个指针 pA 和 pB，分别初始化为链表 A 和 B 的头结点。然后让它们向后逐结点遍历。

2. 当 pA 到达链表的尾部时，将它重定位到链表 B 的头结点 (你没看错，就是链表 B); 类似的，当 pB 到达链表的尾部时，将它重定位到链表 A 的头结点。

3. 若在某一时刻 pA 和 pB 相遇(相等但不为空指针)，则 pA/pB 为相交结点。


<img src="./imglinklist/02-160.png" width=700>

[图片来源](https://leetcode-cn.com/problems/intersection-of-two-linked-lists/solution/tu-jie-xiang-jiao-lian-biao-by-user7208t/)

```java
public class Solution {
    public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
        if(headA==null || headB==null) return null;
        ListNode pA = headA, pB = headB;
        while (pA!=pB){
            pA = pA==null? headB:pA.next;
            pB = pB==null? headA:pB.next;
        }
        return pA;
    }
}
```

### 哈希表法

遍历链表 A 并将每个结点的地址/引用存储在哈希表中。然后检查链表 B 中的每一个结点 b\_i 是否在哈希表中。若在，则 b\_i 为相交结点。

复杂度分析

* 时间复杂度 : O(m+n)。
* 空间复杂度 : O(m) 或 O(n)。

