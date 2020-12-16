## 2 最大子序和


给定一个整数数组 nums ，找到一个具有最大和的连续子数组（子数组最少包含一个元素），返回其最大和。

```
示例:
输入: [-2,1,-3,4,-1,2,1,-5,4]
输出: 6
解释: 连续子数组 [4,-1,2,1] 的和最大，为 6。
```

进阶:如果你已经实现复杂度为 O(n) 的解法，尝试使用更为精妙的分治法求解。


[53. 最大子序和](https://leetcode-cn.com/problems/maximum-subarray/)


### 遍历


思路：当前子序和小于 0，则清空。因为负数与任何数相加都会比该数小。


```java
class Solution {
    public int maxSubArray(int[] nums) {
        if(nums==null || nums.length==0) return 0;
        int maxres = Integer.MIN_VALUE;
        int tempMax = 0;
        for(int i=0; i<nums.length; i++){
            tempMax = tempMax + nums[i];
            maxres = Math.max(tempMax, maxres);
            if(tempMax<0){
                tempMax = 0;
            }
        }
        return maxres;
    }
}
```

### 动态规划

1）设 nums 数组的长度是 n，下标从 0 到 n−1。用 a_i 代表 nums[i]，用 f(i) 代表以第 i 个数**结尾**的「连续子数组的最大和」


2）求 `f(i)`：考虑 `a_i` 单独成为一段还是加入 `f(i−1)` 对应的那一段，这取决于 `a_i` 和 `f(i - 1) + a_i` 的大小。动态规划转移方程为：

    `f(i)=max{f(i−1)+a_i ,a_i}`


```java
class Solution {
    public int maxSubArray(int[] nums) {
        int pre = 0, maxv = nums[0];
        for(int x : nums){
            pre = Math.max(pre+x, x); //f(i)
            maxv = Math.max(pre, maxv);
        }
        return maxv;
    }
}
```

复杂度

* 时间复杂度：O(n)，其中 n 为 nums 数组的长度。只需要遍历一遍数组即可求得答案。

* 空间复杂度：O(1)。只需要常数空间存放若干变量。

### 分治

思路：定义一个操作 get(a, l, r) 表示查询 a 序列 [l, r] 区间内的最大子段和，那么最终要求的答案就是 get(nums, 0, nums.size() - 1)。分治实现，





