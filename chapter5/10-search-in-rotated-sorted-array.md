## 10 搜索旋转排序数组

升序排列的整数数组 nums 在预先未知的某个点上进行了旋转（例如， [0,1,2,4,5,6,7] 经旋转后可能变为 [4,5,6,7,0,1,2] ）。

请你在数组中搜索 target ，如果数组中存在这个目标值，则返回它的索引，否则返回 -1 。

 
```
示例 1：
输入：nums = [4,5,6,7,0,1,2], target = 0
输出：4

示例 2：
输入：nums = [4,5,6,7,0,1,2], target = 3
输出：-1

示例 3：
输入：nums = [1], target = 0
输出：-1
```

提示：
* `1 <= nums.length <= 5000`
* `-10^4 <= nums[i] <= 10^4`
* nums 中的【每个值都独一无二】🍒
* nums 肯定会在某个点上旋转
* `-10^4 <= target <= 10^4`

[33. 搜索旋转排序数组](https://leetcode-cn.com/problems/search-in-rotated-sorted-array/)



### 二分搜索

思路：二分搜索查看当前 mid 为分割位置分割出来的两个部分 [l, mid] 和 [mid + 1, r] 哪个部分是有序的，并根据有序的那个部分确定该如何改变二分搜索的上下界，因为能够根据有序的那部分判断出 target 在不在这个部分：

* 如果 [l, mid - 1] 是有序数组，且 target 的大小满足 [nums[l],nums[mid])，则应该将搜索范围缩小至 [l, mid - 1]，否则在 [mid + 1, r] 中寻找。

* 如果 [mid, r] 是有序数组，且 target 的大小满足 [nums[mid+1],nums[r]]，则应该将搜索范围缩小至 [mid + 1, r]，否则在 [l, mid - 1] 中寻找。


```java
class Solution {
    public int search(int[] nums, int target) {
        int n = nums.length;
        if(nums==null || n==0) return -1;
        int l = 0, r = n - 1;
        while (l<=r){
            int mid = (l+r)/2;
            if(nums[mid]==target) return mid;

            if(nums[l]<=nums[mid]){
                //0~mid为有序部分
                if(nums[l]<=target && target<=nums[mid]){
                    r = mid -1;
                }else{
                    l = mid + 1;
                }
            }else{
                if(nums[mid]<=target && target <=nums[r]){
                    l = mid + 1;
                }else {
                    r = mid -1;
                }
            }
        }
        return -1;
    }
}
```

复杂度分析

* 时间复杂度： O(logn)，其中 nn 为 nums[] 数组的大小。整个算法时间复杂度即为二分搜索的时间复杂度 O(logn)。

* 空间复杂度：O(1) 。只需要常数级别的空间存放变量。
