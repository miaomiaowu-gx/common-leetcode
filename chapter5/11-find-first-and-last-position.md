## 11 在排序数组中查找元素的第一个和最后一个位置


给定一个按照升序排列的整数数组 nums，和一个目标值 target。找出给定目标值在数组中的开始位置和结束位置。

如果数组中不存在目标值 target，返回 [-1, -1]。

进阶：你可以设计并实现时间复杂度为 O(log n) 的算法解决此问题吗？
 

示例 1：

输入：nums = [5,7,7,8,8,10], target = 8
输出：[3,4]
示例 2：

输入：nums = [5,7,7,8,8,10], target = 6
输出：[-1,-1]
示例 3：

输入：nums = [], target = 0
输出：[-1,-1]
 

提示：
* `0 <= nums.length <= 105`
* `-109 <= nums[i] <= 109`
* nums 是一个【非递减数组】🍒
* `-109 <= target <= 109`



[34. 在排序数组中查找元素的第一个和最后一个位置](https://leetcode-cn.com/problems/find-first-and-last-position-of-element-in-sorted-array/)



### 二分查找



思路：由于数组已经排序，因此整个数组是单调递增的，可以利用二分法来加速查找的过程。考虑 target 开始和结束位置，其实要找的就是数组中「第一个等于 target 的位置」（记为 leftIdx）和「第一个大于 target 的位置减一」（记为 rightIdx）。

* 二分查找中，寻找 leftIdx 即为在数组中寻找第一个【大于等于】 target 的下标，寻找 rightIdx 即为在数组中寻找第一个【大于】 target 的下标，然后将下标减一。两者的判断条件不同，为了代码的复用，定义 binarySearch(nums, target, lower) 表示在 nums 数组中二分查找target 的位置，如果 lower 为 true，则查找第一个大于等于 target 的下标，否则查找第一个大于 target 的下标。

* 最后，因为 target 可能不存在数组中，因此需要重新校验得到的两个下标 leftIdx 和 rightIdx，看是否符合条件，如果符合条件就返回 [leftIdx,rightIdx]，不符合就返回 [−1,−1]。

> * 找左侧第一个 target 时，target<=nums[mid]
> * 找右侧第一个比 target 大的数时，target<nums[mid]


```java
class Solution {
    public int[] searchRange(int[] nums, int target) {
        int leftIndex = binarySearch(nums, target, true);
        int rightIndex = binarySearch(nums, target, false)-1;
        if(leftIndex<=rightIndex && rightIndex<nums.length && nums[leftIndex]==target && nums[rightIndex]==target){
            return new int[]{leftIndex,rightIndex};
        }
        return new int[]{-1,-1};
    }

    public int binarySearch(int[] nums, int target, boolean lower){
        int left = 0, right = nums.length-1;
        while (left<=right){
            int mid = (left+right)/2;
            if(target<nums[mid] || (lower && target<=nums[mid])){
                //找左侧第一个target时，target<=nums[mid]
                //找右侧第一个比target大的数时，target<nums[mid]
                right = mid - 1;
            }else{
                left = mid + 1;
            }
        }
        return left;
    }
}
```


复杂度分析

* 时间复杂度：(logn)，其中 n 为数组的长度。二分查找的时间复杂度为 O(logn)，一共会执行两次，因此总时间复杂度为 O(logn)。

* 空间复杂度：O(1)。只需要常数空间存放若干变量。


### 二分查找-实现 2

```java
class Solution {
    public int[] searchRange(int[] nums, int target) {
        int len = nums.length;
        if (len == 0) {
            return new int[]{-1, -1};
        }

        int firstPosition = findFirstPosition(nums, target);
        if (firstPosition == -1) {
            return new int[]{-1, -1};
        }

        int lastPosition = findLastPosition(nums, target);
        return new int[]{firstPosition, lastPosition};
    }

    // 查找第一个等于target的位置.
    // 因此找到等于时，不直接返回，而是缩小右侧空间，right=mid.
    // 继续查找，左侧仍然可能存在 target.
    private int findFirstPosition(int[] nums, int target) {
        int left = 0;
        int right = nums.length - 1;
        while (left < right) {
            int mid = left + (right - left) / 2;
            // 小于一定不是解
            if (nums[mid] < target) {
                // 下一轮搜索区间是 [mid + 1, right]
                left = mid + 1;
            } else if (nums[mid] == target) {
                // 下一轮搜索区间是 [left, mid]
                right = mid;
            } else {
                // nums[mid] > target，下一轮搜索区间是 [left, mid - 1]
                right = mid - 1;
            }
        }

        if (nums[left] == target) {
            return left;
        }
        return -1;
    }

    // 找最后一个target位置.
    // 因此找到等于时，不直接返回，而是缩小左侧空间，left=mid.
    // 继续查找，右侧仍然可能存在 target.
    private int findLastPosition(int[] nums, int target) {
        int left = 0;
        int right = nums.length - 1;
        while (left < right) {
            int mid = left + (right - left + 1) / 2;
            if (nums[mid] > target) {
                // 下一轮搜索区间是 [left, mid - 1]
                right = mid - 1;
            } else if (nums[mid] == target){
                // 下一轮搜索区间是 [mid, right]
                left = mid;
            } else {
                // nums[mid] < target，下一轮搜索区间是 [mid + 1, right]
                left = mid + 1;
            }
        }
        return left;
    }
}
```

复杂度分析：

* 时间复杂度：O(logN)，这里 N 是数组的长度，两个子问题都是二分查找，因此时间复杂度为对数级别；

* 空间复杂度：O(1)，只使用了常数个数的辅助变量、指针。




