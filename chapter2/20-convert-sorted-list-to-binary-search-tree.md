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

设当前链表的左端点为 left，右端点 right，包含关系为「左闭右开」，即 left 包含在链表中而 right 不包含在链表中。由「快慢指针法」找出链表的中位数节点 mid。


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


### 