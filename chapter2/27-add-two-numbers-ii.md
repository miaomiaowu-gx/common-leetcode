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

复杂度分析

* 时间复杂度：O(max(m,n))，其中 m 与 n 分别为两个链表的长度。需要遍历每个链表。

* 空间复杂度：O(m+n)，其中 m 与 n 分别为两个链表的长度。这是把链表内容放入栈中所用的空间。



### 链表逆序相加

反转后相加再反转

```java
class Solution {
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        l1 = reverse(l1);
        l2 = reverse(l2);
        ListNode ans = addTwoNumbersCore(l1,l2);
        ans = reverse(ans);
        return ans;
    }
    public ListNode addTwoNumbersCore(ListNode l1, ListNode l2){
        int carry  = 0;
        ListNode res = new ListNode(-1), p=res;
        while (l1!=null || l2!=null || carry!=0){
            int val1 = l1==null ? 0 : l1.val;
            int val2 = l2==null ? 0 : l2.val;
            int cur = val1 + val2 + carry;
            carry = cur / 10;
            cur = cur % 10;
            p.next = new ListNode(cur);
            p = p.next;
            l1 = l1==null? null:l1.next;
            l2 = l2==null? null:l2.next;
        }
        return res.next;
    }

    public ListNode reverse(ListNode head) {
        if(head==null) return head;
        ListNode prev = null;
        while (head!=null){
            ListNode t = head.next;
            head.next = prev;
            prev = head;
            head = t;
        }
        return prev;
    }

}
```

### 不修改输入链表-不用栈-不用递归 🍒


思路：两个链表长度对齐之后每位加和生成新链表，之后反转新链表，边反转边计算进位

```java
class Solution {

    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        int length1 = lengthOf(l1);
        int length2 = lengthOf(l2);
        if (length1 > length2) {
            return addTwoNumbers(l1,l2,length1 - length2);
        }else {
            return addTwoNumbers(l2,l1,length2 - length1);
        }
    }

    ListNode addTwoNumbers(ListNode theLong, ListNode theShort, int diff) {
        ListNode head = null;
        //头插法，长链表比短链表多出的节点表示高位，先直接放入新链表
        while (diff > 0) {
            ListNode node = new ListNode(theLong.val);
            node.next = head;
            head = node;
            theLong = theLong.next;
            diff--;
        }
        //两个链表对齐之后开始加和，先不进位，因为进位需要从低往高位走，现在是从高位往低位走
        //直接保存加和结果
        while (null != theLong) {
            ListNode node = new ListNode(theLong.val + theShort.val);
            node.next = head;
            head = node;
            theLong = theLong.next;
            theShort = theShort.next;
        }
        //头插法结束，链表指针方向为从低位到高位
        //因为进位是从低位往高位走，所以边反转边进位
        ListNode pre = null;
        ListNode cur = head;
        int overflow = 0;
        while (null != cur) {
            int sum = cur.val + overflow;
            overflow = sum /10;
            sum = sum %10;
            cur.val = sum; //赋上进位之后该节点的值
            //以下代码主要是反转新链表
            ListNode temp = cur.next;
            cur.next = pre;
            pre = cur;
            cur = temp;
        }
        //最后一个节点产生了进位，则要在高位头插一个节点
        if (overflow>0) {
            ListNode node = new ListNode(overflow);
            node.next = pre;
            pre = node;
        }
        //新链表反转加进位之后得到 1->3->0->2
        return pre;
    }

    int lengthOf(ListNode l) {
        int length = 0;
        while (null != l) {
            length++;
            l = l.next;
        }
        return length;
    }
}
```




