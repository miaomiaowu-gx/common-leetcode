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





