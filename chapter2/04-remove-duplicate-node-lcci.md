## 4 删除非排序链表中的重复元素


编写代码，移除**未排序**链表中的重复节点。保留最开始出现的节点。

示例1:

```
输入：[1, 2, 3, 3, 2, 1]
输出：[1, 2, 3]
``` 
 
示例2:

```
输入：[1, 1, 1, 1, 2]
输出：[1, 2]
```

提示：
* 链表长度在[0, 20000]范围内。
* 链表元素在[0, 20000]范围内。

进阶：如果不得使用临时缓冲区，该怎么解决？


[面试题 02.01. 移除重复节点](https://leetcode-cn.com/problems/remove-duplicate-node-lcci/)

### 方法一：哈希表

对给定的链表进行一次遍历，并用一个哈希集合（HashSet）来存储所有出现过的节点。从链表的头节点 head 开始进行遍历，遍历的指针记为 pos。由于头节点一定不会被删除，因此可以枚举待移除节点的前驱节点，减少编写代码的复杂度。

```java
class Solution {
    public ListNode removeDuplicateNodes(ListNode head) {
        if (head == null) {
            return head;
        }
        Set<Integer> occurred = new HashSet<Integer>();
        occurred.add(head.val);
        ListNode pos = head;
        // 枚举前驱节点
        while (pos.next != null) {
            // 当前待删除节点
            ListNode cur = pos.next;
            if (occurred.add(cur.val)) {
                pos = pos.next;
            } else {
                pos.next = pos.next.next;
            }
        }
        return head;
    }
}
```

复杂度分析

* 时间复杂度：O(N)，其中 N 是给定链表中节点的数目。

* 空间复杂度：O(N)。在最坏情况下，给定链表中每个节点都不相同，哈希表中需要存储所有的 N 个值。


### 方法二：两重循环


思路 1：一种简单的方法是，在给定的链表上使用两重循环，其中第一重循环从链表的头节点开始，枚举一个保留的节点，因为保留的是「最开始出现的节点」。第二重循环从枚举的保留节点开始，到链表的末尾结束，将所有与保留节点相同的节点全部移除。


思路 2：第一重循环枚举保留的节点本身，而为了编码方便，第二重循环可以枚举待移除节点的前驱节点，方便对节点进行移除。这样一来，使用「时间换空间」的方法，就可以不使用临时缓冲区。

