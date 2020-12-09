## 10 环形链表 II

给定一个链表，返回链表开始入环的第一个节点。 如果链表无环，则返回 null。

为了表示给定链表中的环，我们使用整数 pos 来表示链表尾连接到链表中的位置（索引从 0 开始）。 如果 pos 是 -1，则在该链表中没有环。注意，pos 仅仅是用于标识环的情况，并不会作为参数传递到函数中。

说明：不允许修改给定的链表。

进阶：你是否可以使用 O(1) 空间解决此题？


[142.环形链表 II](https://leetcode-cn.com/problems/linked-list-cycle-ii/)


### 快慢指针

快慢指针相遇，则有环。

确定环的位置，让其中一个指针从头节点开始，另一个指针从相遇节点开始，两者同时开始移动。再次相遇则为环的起始点！


```java
public class Solution {
    public ListNode detectCycle(ListNode head) {
        ListNode two = head, one = head;
        while (two!=null && two.next!=null){
            two = two.next.next;
            one = one.next;
            if(two == one){
                //有环
                one = head;
                while(one != two){
                    one = one.next;
                    two = two.next;
                }
                return one;
            }
        }
        return null;
    }
}
```