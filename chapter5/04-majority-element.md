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


### 



### 




### 





### 















