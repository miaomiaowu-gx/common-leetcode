## 3 删除排序链表中的重复元素


给定一个**排序链表**，删除所有重复的元素，使得每个元素只出现一次。

示例 1:

```
输入: 1->1->2
输出: 1->2
```

示例 2:

```
输入: 1->1->2->3->3
输出: 1->2->3
```


[题目链接](https://leetcode-cn.com/problems/remove-duplicates-from-sorted-list/)

### 实现1

思路：当前元素与下一个元素相等，则删除当前元素。


缺点：不需要那么多指针！


```java
class Solution {
    public ListNode deleteDuplicates(ListNode head) {
        ListNode newHead = new ListNode(-1);
        newHead.next = head;
        ListNode pre = newHead;

        while(head != null && head.next != null){
            if(head.val == head.next.val){
                pre.next = head.next;
            }else{
                pre = head;
            }
            head = head.next;
        }
        return newHead.next;
    }
}
```


### 实现2

思路：当前元素与下一个元素相等，则删除下一个元素。


```java
class Solution {
    public ListNode deleteDuplicates(ListNode head) {
        ListNode current = head;
        while (current != null && current.next != null) {
            if (current.next.val == current.val) {
                current.next = current.next.next;
            } else {
                current = current.next;
            }
        }
        return head;
    }
}
```


复杂度分析

* 时间复杂度：O(n)，因为列表中的每个结点都检查一次以确定它是否重复，所以总运行时间为 O(n)，其中 n 是列表中的结点数。

* 空间复杂度：O(1)，没有使用额外的空间。



