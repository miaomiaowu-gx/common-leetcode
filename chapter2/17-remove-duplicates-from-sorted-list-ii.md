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

双指针的方式，定义a，b两个指针。

* 考虑到一些边界条件，比如 1->1->1->2 这种情况，需要把开头的几个 1 给去掉，增加一个哑结点(头头节点)，方便边界处理。

* 初始的两个指针，将 a 指针指向哑结点，将 b 指针指向 head (哑结点的下一个节点)。

* 如果 a 的 next 指向的值不等于 b 的 next 指向的值，则两个指针都前进一位
否则，就单独移动 b，b 不断往前走，直到 a 的 next 指向的值不等于 b 的 next 指向的值。



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
