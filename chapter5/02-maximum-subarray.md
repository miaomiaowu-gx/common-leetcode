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

思路：定义一个操作 get(a, l, r) 表示查询 a 序列 [l, r] 区间内的最大子段和，那么最终要求的答案就是 get(nums, 0, nums.size() - 1)。分治实现，对于一个区间 [l, r]，取 m = (l+r)/2，对区间 [l, m]「左子区间」 和 [m + 1, r] 「右子区间」分治求解。当递归逐层深入直到区间长度缩小为 1 的时候，递归「开始回升」。考虑如何通过 [l, m] 区间的信息和 [m + 1, r] 区间的信息合并成区间 [l, r] 的信息。

维护四个量：

* lSum 表示 [l, r] 内以 l 为左端点的最大子段和
* rSum 表示 [l, r] 内以 r 为右端点的最大子段和
* mSum 表示 [l, r] 内的最大子段和
* iSum 表示 [l, r] 的区间和


1）对于长度为 1 的区间 [i, i]，四个量的值都和 a_i 相等。

2）对于长度大于 1 的区间

* 首先最好维护的是 iSum，区间 [l, r] 的 iSum 就等于「左子区间」的 iSum 加上「右子区间」的 iSum。


* 对于 [l, r] 的 lSum，存在两种可能，它要么等于「左子区间」的 lSum，要么等于「左子区间」的 iSum 加上「右子区间」的 lSum，二者取大。


* 对于 [l, r] 的 rSum，同理，它要么等于「右子区间」的 rSum，要么等于「右子区间」的 iSum 加上「左子区间」的 rSum，二者取大。


* 考虑 [l, r] 的 mSum 对应的区间是否跨越 m

  * 它可能不跨越 m，也就是说 [l, r] 的 mSum 可能是「左子区间」的 mSum 和 「右子区间」的 mSum 中的一个；
  * 它也可能跨越 m，可能是「左子区间」的 rSum 和 「右子区间」的 lSum 求和。
  * 三者取大。


```java
class Solution {
    public class Status{
        public int lSum, rSum, mSum, iSum;
        public Status(int lSum,int rSum,int mSum,int iSum){
            this.lSum = lSum;
            this.rSum = rSum;
            this.mSum = mSum;
            this.iSum = iSum; //区间和
        }
    }
    public int maxSubArray(int[] nums) {
        return getInfo(nums,0,nums.length-1).mSum;
    }

    public Status getInfo(int[] a, int l, int r){
        if(l==r){
            return new Status(a[r],a[r],a[r],a[r]);
        }
        int mid = (l+r)/2;
        Status sl =  getInfo(a,l,mid);
        Status sr =  getInfo(a,mid+1,r);
        return pushUp(sl,sr);
    }

    public Status pushUp(Status l, Status r){
        int iSum = l.iSum + r.iSum;
        int lSum = Math.max(l.lSum, l.iSum+r.lSum);
        int rSum = Math.max(r.rSum, r.iSum+l.rSum);
        int mSum = Math.max(l.mSum,r.mSum);
        mSum = Math.max(mSum,l.rSum+r.lSum);
        return new Status(lSum,rSum,mSum,iSum);
    }
}
```









