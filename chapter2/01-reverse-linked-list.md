## 1 反转链表


反转一个单链表。

示例:

```
输入: 1->2->3->4->5->NULL
输出: 5->4->3->2->1->NULL
```

进阶：可以迭代或递归地反转链表。你能否用两种方法解决这道题？

[206. 反转链表](https://leetcode-cn.com/problems/reverse-linked-list/)

### 迭代反转链表

假设存在链表 1→2→3→∅，想要把它改成 ∅←1←2←3。

在遍历列表时，将当前节点的 next 指针改为指向前一个元素。由于节点没有引用其上一个节点，因此必须事先存储其前一个元素。在更改引用之前，还需要另一个指针来存储下一个节点。不要忘记在最后返回新的头引用！


```java
class Solution {
    public ListNode reverseList(ListNode head) {
        ListNode pre = null;
        ListNode curr = head;
        while(curr != null){
            ListNode tmpNext = curr.next;
            curr.next = pre;
            pre = curr;
            curr = tmpNext;
        }
        return pre;
    }
}
```


复杂度分析

* 时间复杂度：O(n)，假设 n 是列表的长度，时间复杂度是 O(n)。

* 空间复杂度：O(1)。

### 递归反转链表

假设列表的其余部分已经被反转，现在应该如何反转它前面的部分？


若从节点 n\_{k+1} 已经被反转，现在处于 n\_{k}。
	
`n\_{1} ->...-> n\_{k-1} -> n\_{k} -> n\_{k+1} <-...<- n\_{m}` 

希望 n\_{k+1} 的下一个节点指向 n\_{k}。

所以，n\_{k}.next.next = n\_{k}。

要小心的是 n_{1} 的下一个必须指向 ∅ 。如果你忽略了这一点，链表中可能会产生循环。如果使用大小为 2 的链表测试代码，则可能会捕获此错误。

```java
class Solution {
    public ListNode reverseList(ListNode head) {
        if(head == null || head.next == null)
            return head;
        ListNode newHead = reverseList( head.next );
        head.next.next = head;
        head.next = null;
        return newHead;
    }
}
```



复杂度分析

* 时间复杂度：O(n)，假设 n 是列表的长度，那么时间复杂度为 O(n)。

* 空间复杂度：O(n)，由于使用递归，将会使用隐式栈空间。递归深度可能会达到 n 层。




