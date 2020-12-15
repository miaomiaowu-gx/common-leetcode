## 27 两数相加 II

给你两个 非空 链表来代表两个非负整数。数字最高位位于链表开始位置。它们的每个节点只存储一位数字。将这两数相加会返回一个新的链表。

可以假设除了数字 0 之外，这两个数字都不会以零开头。

进阶：如果输入链表不能修改该如何处理？换句话说，你不能对列表中的节点进行翻转。

 
```
示例：
输入：(7 -> 2 -> 4 -> 3) + (5 -> 6 -> 4)
输出：7 -> 8 -> 0 -> 7
```

[445. 两数相加 II](https://leetcode-cn.com/problems/add-two-numbers-ii/)


### 栈

对于逆序处理首先想到栈，把所有数字压入栈中，再依次取出相加。计算过程中需要注意进位的情况。

```java
class Solution {
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        Stack<Integer> stack1 = new Stack<Integer>();
        Stack<Integer> stack2 = new Stack<Integer>();
        while (l1!=null){
            stack1.push(l1.val);
            l1 = l1.next;
        }
        while (l2!=null){
            stack2.push(l2.val);
            l2 = l2.next;
        }
        ListNode ans = null;
        int carry = 0;
        while (!stack1.isEmpty() || !stack2.isEmpty() || carry!=0){
            int val1 = stack1.isEmpty()? 0:stack1.pop();
            int val2 = stack2.isEmpty()? 0:stack2.pop();
            int cur = val1+val2+carry;
            carry = cur/10;
            cur = cur % 10;
            ListNode curNode = new ListNode(cur);
            curNode.next = ans;
            ans = curNode;
        }
        return ans;
    }
}
```


