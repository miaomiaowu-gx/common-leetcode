## 12 回文链表


请判断一个链表是否为回文链表。

```
示例 1:
输入: 1->2
输出: false

示例 2:
输入: 1->2->2->1
输出: true
```

进阶：你能否用 O(n) 时间复杂度和 O(1) 空间复杂度解决此题？


[234. 回文链表](https://leetcode-cn.com/problems/palindrome-linked-list/)


### 方法一：将值复制到数组中后用双指针法

```java
class Solution {
    public boolean isPalindrome(ListNode head) {
        ArrayList<Integer> arr = new ArrayList<>();
        ListNode curr = head;
        while (curr!=null){
            arr.add(curr.val);
            curr = curr.next;
        }

        int front = 0, back = arr.size()-1;
        while (front<back){
            if(!arr.get(front).equals(arr.get(back))){
                return false;
            }
            front++;
            back--;
        }
        return true;
    }
}
```


复杂度分析

* 时间复杂度：O(n)，其中 n 指的是链表的元素个数。

  * 第一步： 遍历链表并将值复制到数组中，O(n)。

  * 第二步：双指针判断是否为回文，执行了 O(n/2) 次的判断，即 O(n)。
  
  * 总的时间复杂度：O(2n) = O(n)。

* 空间复杂度：O(n)，其中 n 指的是链表的元素个数，我们使用了一个数组列表存放链表的元素值。

### 方法二：递归



### 方法三：快慢指针


