## 17 删除排序链表中的重复元素 II


给定一个**排序**链表，删除所有含有重复数字的节点，只保留原始链表中 没有重复出现 的数字。

```
示例 1:

输入: 1->2->3->3->4->4->5
输出: 1->2->5

示例 2:

输入: 1->1->1->2->3
输出: 2->3
```



[82. 删除排序链表中的重复元素 II](https://leetcode-cn.com/problems/remove-duplicates-from-sorted-list-ii/)

### 迭代





```java
class Solution {
    public ListNode deleteDuplicates(ListNode head) {
        if(head==null || head.next==null) {
            return head;
        }
        ListNode newHead = new ListNode(-1);
        newHead.next = head;

        ListNode a = newHead;
        ListNode b = head;

        while (b!=null && b.next!=null){
            if(a.next.val!=b.next.val){
                a = a.next;
                b = b.next;
            }else{
                while (b!=null && b.next!=null && a.next.val==b.next.val){
                    b = b.next;
                }
                a.next = b.next;
                b = b.next;
            }
        }
        return newHead.next;
    }
}
```


### 递归

思路：判断头结点是否有重复元素

```java
class Solution {
    public ListNode deleteDuplicates(ListNode head) {
        if(head==null || head.next==null) return head;

        //当前链表头节点有重复
        if(head.val == head.next.val){
            while (head!=null && head.next!=null && head.val == head.next.val){
                head = head.next;
            }
            return deleteDuplicates(head.next);
        }else{ //头节点没有重复
            head.next = deleteDuplicates(head.next);
            return head;
        }
    }
}
```
