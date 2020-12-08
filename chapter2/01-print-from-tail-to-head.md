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

复杂性分析

* 时间复杂度：O(n)。正向遍历一遍链表，然后从栈弹出全部节点，等于又反向遍历一遍链表。

* 空间复杂度：O(n)。额外使用一个栈存储链表中的每个节点。


#### 2）递归

思路：利用递归，先走至链表末端，回溯时依次将节点值加入列表 ，这样就可以实现链表值的倒序输出。

参考使用递归逆序打印一个链表：

```java
public void reversePrint(ListNode head) {
    if (head == null)
        return;
    //先逆序打印后部分链表    
    reversePrint(head.next);
    //再打印当前
    System.out.println(head.val);
}
```





#### 3）反转链表 🍒









