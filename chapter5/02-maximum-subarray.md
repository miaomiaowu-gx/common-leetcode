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

