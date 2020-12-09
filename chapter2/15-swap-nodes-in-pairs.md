## 15 两两交换链表中的节点


给定一个链表，两两交换其中相邻的节点，并返回交换后的链表。不能只是单纯的改变节点内部的值，而是需要实际的进行节点交换。

```
示例 1：
输入：head = [1,2,3,4]
输出：[2,1,4,3]

示例 2：
输入：head = []
输出：[]

示例 3：
输入：head = [1]
输出：[1]
```


[24. 两两交换链表中的节点](https://leetcode-cn.com/problems/swap-nodes-in-pairs/)


### 迭代

思路：建立头头节点，每次交换当前节点后的两个节点


```java
class Solution {
    public ListNode swapPairs(ListNode head) {
        if(head==null){
            return head;
        }
        ListNode newHead = new ListNode(-1,head), p =  newHead;
        //每次需要交换 p 后面的两个节点
        while (p!=null && p.next!=null && p.next.next!=null){
            ListNode node1 = p.next;
            ListNode node2 = p.next.next;
            node1.next = node2.next;
            node2.next = node1;
            p.next = node2;
            p = p.next.next;
        }
        return newHead.next;
    }
}
```

复杂度分析

* 时间复杂度：O(n)，其中 n 是链表的节点数量。需要对每个节点进行更新指针的操作。

* 空间复杂度：O(1)。

### 递归


递归的终止条件是链表中没有节点，或者链表中只有一个节点，此时无法进行交换。

算法思路：

1. 如果链表中至少有两个节点，则在两两交换链表中的节点之后，原始链表的头节点变成新的链表的第二个节点，原始链表的第二个节点变成新的链表的头节点。

2. 链表中的其余节点的两两交换可以递归地实现。

3. 在对链表中的其余节点递归地两两交换之后，更新节点之间的指针关系，即可完成整个链表的两两交换。

4. 递归的终止条件是链表中没有节点，或者链表中只有一个节点，此时无法进行交换。

```java
class Solution {
    public ListNode swapPairs(ListNode head) {
        if (head == null || head.next == null) {
            return head;
        }
        ListNode newHead = head.next;
        head.next = swapPairs(newHead.next);
        newHead.next = head;
        return newHead;
    }
}
```

复杂度分析

* 时间复杂度：O(n)，其中 n 是链表的节点数量。需要对每个节点进行更新指针的操作。

* 空间复杂度：O(n)，其中 n 是链表的节点数量。空间复杂度主要取决于递归调用的栈空间。

