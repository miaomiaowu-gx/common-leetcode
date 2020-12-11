## 20 有序链表转换二叉搜索树

给定一个单链表，其中的元素按升序排序，将其转换为高度平衡的二叉搜索树。

本题中，一个高度平衡二叉树是指一个二叉树每个节点 的左右两个子树的高度差的绝对值不超过 1。

示例:

```
给定的有序链表： [-10, -3, 0, 5, 9],

一个可能的答案是：[0, -3, 9, -10, null, 5], 它可以表示下面这个高度平衡二叉搜索树：

      0
     / \
   -3   9
   /   /
 -10  5
```

[题解](https://leetcode-cn.com/problems/convert-sorted-list-to-binary-search-tree/)



### 分治

思路：将给定的有序链表转换为二叉搜索树的第一步是确定根节点。需要构造出平衡的二叉树，即根节点左子树中的节点个数与右子树中的节点个数尽可能接近。找出链表元素的中位数作为根节点的值。(如果元素个数为偶数，那么唯二的中间值都可以作为中位数，而不是常规定义中二者的平均值。)根据中位数的性质，链表中小于中位数的元素个数与大于中位数的元素个数要么相等，要么相差 1。此时，小于中位数的元素组成了左子树，大于中位数的元素组成了右子树，它们分别对应着有序链表中连续的一段。在这之后，使用分治的思想，继续递归地对左右子树进行构造，找出对应的中位数作为根节点，以此类推。

设当前链表的左端点为 left，右端点 right，**包含关系为「左闭右开」**，即 left 包含在链表中而 right 不包含在链表中。由「快慢指针法」找出链表的中位数节点 mid。


```java
class Solution {
    public TreeNode sortedListToBST(ListNode head) {
        return buildTree(head,null);
    }

    public TreeNode buildTree(ListNode left, ListNode right){
        if(left==right) return null;

        ListNode mid = getMedian(left, right);
        TreeNode root = new TreeNode(mid.val);
        root.left = buildTree(left, mid);
        root.right = buildTree(mid.next, right);
        return root;
    }

    //偶数，取后一个为中间数
    public ListNode getMedian(ListNode left, ListNode right){
        ListNode slow = left, fast = left;
        while (fast!=right && fast.next!=right){
            fast = fast.next.next;
            slow = slow.next;
        }
        return slow;
    }
}
```


复杂度分析

* 时间复杂度：O(nlogn)，其中 n 是链表的长度。

  * 设长度为 n 的链表构造二叉搜索树的时间为 T(n)，递推式为 T(n)=2⋅T(n/2)+O(n)，根据主定理，T(n)=O(nlogn)。

* 空间复杂度：O(logn)，这里只计算除了返回答案之外的空间。平衡二叉树的高度为 O(logn)，即为递归过程中栈的最大深度，也就是需要的空间。


> **为什么要设定「左闭右开」的关系？**由于题目中给定的链表为单向链表，访问后继元素十分容易，但无法直接访问前驱元素。因此在找出链表的中位数节点 mid 之后，如果设定「左闭右开」的关系，就可以直接用 (left,mid) 以及 (mid.next,right) 来表示左右子树对应的列表。并且，初始的列表也可以用 (head, null) 方便地进行表示，其中 null 表示空节点。


### 分治 + 中序遍历优化

没有必要“先”找到中间节点：可以先构建了左子树，建立结束后，指针自然指向中间结点。那么如何构建左子树呢？只需要确定子树的大小就可以。所以先用O(n)的时间计算链表长度，之后用中序遍历(左根右)。当然，指针需要是“引用”。


1. 由于构造出的二叉搜索树的中序遍历结果就是链表本身，因此可以将分治和中序遍历结合起来，减少时间复杂度。

2. 具体地，设当前链表的左端点编号为 left，右端点编号为 right，包含关系为「双闭」，即 left 和 right 均包含在链表中。链表节点的编号为 [0,n)。中序遍历的顺序是「左子树 - 根节点 - 右子树」，那么在分治的过程中，不用急着找出链表的中位数节点，而是使用一个占位节点，等到中序遍历到该节点时，再填充它的值。

3. 中位数节点对应的编号为 mid=(left+right+1)/2；

4. 左右子树对应的编号范围分别为 [left,mid−1] 和 [mid+1,right]。

5. 如果 left>right，那么遍历到的位置对应着一个空节点，否则对应着二叉搜索树中的一个节点。

6. 