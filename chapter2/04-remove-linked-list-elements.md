## 4 移除值为 val 的链表元素


删除链表中等于给定值 val 的所有节点。

示例:

```
输入: 1->2->6->3->4->5->6, val = 6
输出: 1->2->3->4->5
```


[题目 203 链接](https://leetcode-cn.com/problems/remove-linked-list-elements/)


### 题解

思路：头节点有可能被删除，要建立头头节点；删除当前节点需要一直前一个节点，建立节点 pre 记录前一个节点。

```java
class Solution {
    public ListNode removeElements(ListNode head, int val) {
        ListNode newHead = new ListNode(-1);
        newHead.next = head;
        ListNode pre = newHead;
        ListNode curr = head;
        while (curr!=null){
            if(curr.val == val){
                pre.next = curr.next;
            }else{
                pre = curr;
            }
            curr = curr.next;
        }
        return newHead.next;
    }
}
```