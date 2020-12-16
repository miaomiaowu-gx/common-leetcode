## 4 多数元素


给定一个大小为 n 的数组，找到其中的多数元素。多数元素是指在数组中出现次数大于 ⌊ n/2 ⌋ 的元素。

你可以假设数组是非空的，并且给定的数组总是存在多数元素。

 
```
示例 1:
输入: [3,2,3]
输出: 3

示例 2:
输入: [2,2,1,1,1,2,2]
输出: 2
```

[169. 多数元素](https://leetcode-cn.com/problems/majority-element/)

### 哈希表

使用哈希映射（HashMap）来存储每个元素以及出现的次数。对于哈希映射中的每个键值对，键表示一个元素，值表示该元素出现的次数。


```java
class Solution {
    private Map<Integer, Integer> countNums(int[] nums) {
        Map<Integer, Integer> counts = new HashMap<Integer, Integer>();
        for (int num : nums) {
            if (!counts.containsKey(num)) {
                counts.put(num, 1);
            } else {
                counts.put(num, counts.get(num) + 1);
            }
        }
        return counts;
    }

    public int majorityElement(int[] nums) {
        Map<Integer, Integer> counts = countNums(nums);
        Map.Entry<Integer, Integer> maxv = null; //用于记录最大值
        for(Map.Entry<Integer, Integer> cur: counts.entrySet()){
            if(maxv == null || cur.getValue()>maxv.getValue()){
                maxv = cur;
            }
        }
        return maxv.getKey();
    }
}
```

复杂度分析

* 时间复杂度：O(n)。

* 空间复杂度：O(n)。


### 排序

将数组 nums 中的所有元素按照单调递增或单调递减的顺序排序，那么下标为 n/2 的元素一定时众数。

```java
class Solution {
    public int majorityElement(int[] nums) {
        Arrays.sort(nums);
        return nums[nums.length/2];
    }
}
```

复杂度分析

* 时间复杂度：O(nlogn)。将数组排序的时间复杂度为 O(nlogn)。

* 空间复杂度：O(logn)。如果使用语言自带的排序算法，需要使用 O(logn) 的栈空间。如果自己编写堆排序，则只需要使用 O(1) 的额外空间。



### 随机化

算法思路：由于一个给定的下标对应的数字很有可能是众数，随机挑选一个下标，检查它是否是众数，如果是就返回，否则继续随机挑选。

```java
class Solution {
    private int randRange(Random rand, int min, int max) {
        return rand.nextInt(max - min) + min;
    }

    private int countOccurences(int[] nums, int num) {
        int count = 0;
        for (int i = 0; i < nums.length; i++) {
            if (nums[i] == num) {
                count++;
            }
        }
        return count;
    }

    public int majorityElement(int[] nums) {
        Random rand = new Random();

        int majorityCount = nums.length / 2;

        while (true) {
            int candidate = nums[randRange(rand, 0, nums.length)];
            if (countOccurences(nums, candidate) > majorityCount) {
                return candidate;
            }
        }
    }
}
```

复杂度分析

* 时间复杂度：理论上最坏情况下的时间复杂度为 O(∞)。然而，运行的期望时间是线性的。当众数恰好占据数组的一半时，第一次随机有 1/2 的概率找到众数，如果没有找到，则第二次随机时，包含上一次有 1/4 的概率找到众数，以此类推。因此期望的次数为 i/2^i 的和，可以计算出这个和为 2，说明期望的随机次数是常数。每一次随机后，需要 O(n) 的时间判断这个数是否为众数，因此期望的时间复杂度为 O(n)。

* 空间复杂度：O(1)。随机方法只需要常数级别的额外空间。


### 分治

思路：如果数 a 是数组 nums 的众数，将 nums 分成两部分，那么 a 必定是至少其中一个部分的众数。

* 长度为 1 的子数组中唯一的数显然是众数，直接返回。

* 




### 















