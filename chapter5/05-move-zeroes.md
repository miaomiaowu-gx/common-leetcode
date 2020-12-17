## 5 移动零

给定一个数组 nums，编写一个函数将所有 0 移动到数组的末尾，同时保持非零元素的相对顺序。

```
示例:
输入: [0,1,0,3,12]
输出: [1,3,12,0,0]
```

说明:

* 必须在原数组上操作，不能拷贝额外的数组。
* 尽量减少操作次数。

[283. 移动零](https://leetcode-cn.com/problems/move-zeroes/)

### 一次遍历

思路：参考了快速排序的思想，快速排序首先要确定一个待分割的元素做中间点 x，然后把所有小于等于 x 的元素放到 x 的左边，大于 x 的元素放到其右边。用 0 当做这个中间点，把不等于 0 (注意题目没说不能有负数)的放到中间点的左边，等于 0 的放到其右边。

总结：遍历时，非 0 元素交换，0 元素则 i 增加(继续遍历)，j 不变。

<img src="./imgarray/01-05-283.png" width=600>

```java
class Solution {
    public void moveZeroes(int[] nums) {
        if(nums==null) return;
        int j=0;
        for(int i=0; i<nums.length; i++){
            //当前数不为0，则交换i与j
            if(nums[i]!=0){
                int temp = nums[i];
                nums[i] = nums[j];
                nums[j++] = temp;
            }
        }
    }
}
```


### 两次遍历

思路：创建两个指针 i 和 j，第一次遍历的时候指针 j 用来记录当前有多少非 0 元素。即遍历的时候每遇到一个非 0 元素就将其往数组左边挪，第一次遍历完后，j 指针的下标就指向了最后一个非 0 元素下标。第二次遍历的时候，起始位置就从 j 开始到结束，将剩下的这段区域内的元素全部置为 0。

```java
class Solution {
    public void moveZeroes(int[] nums) {
        if(nums==null) return;
        int j=0;
        for(int i=0; i<nums.length; i++){
            if(nums[i]!=0){
                nums[j++] = nums[i];
            }
        }
        for(int i=j; i<nums.length;i++){
            nums[i]=0;
        }
    }
}
```




