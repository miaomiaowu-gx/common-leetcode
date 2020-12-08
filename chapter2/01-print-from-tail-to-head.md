## 1 从尾到头打印链表  

输入一个链表的头节点，从尾到头反过来返回每个节点的值（用数组返回）。

示例 1

```
输入：head = [1,3,2]
输出：[2,3,1]
```

限制：`0 <= 链表长度 <= 10000`。

[题目](https://leetcode-cn.com/problems/cong-wei-dao-tou-da-yin-lian-biao-lcof/)

### 题解

#### 1）栈

思路：把链表的节点全部压栈，因为栈是先进后出的一种数据结构，全部压栈之后再一个个出栈。即实现倒叙！

```java
class Solution {
    public int[] reversePrint(ListNode head) {
        Stack<ListNode> stack = new Stack<ListNode>();
        ListNode temp = head;
        while (temp != null) {
            stack.push(temp);
            temp = temp.next;
        }
        int size = stack.size();
        int[] print = new int[size];
        for (int i = 0; i < size; i++) {
            print[i] = stack.pop().val;
        }
        return print;
    }
}
```


#### 2）递归


#### 3）反转链表🍒









