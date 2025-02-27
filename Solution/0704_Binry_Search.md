# Binary Search / 二分查找

Leetcode: https://leetcode.com/problems/binary-search/description/

中文力扣：https://leetcode.cn/problems/binary-search/description/

## Solution: Binary Search / 二分搜索 

Since the array is sorted, `nums` should be preprocessed first. if` target `is smaller than the first value of `nums` or greater than the last value of `nums`, return -1 directly without performing the search

It is important to determine whether to add or subtract 1 when updating the left and right boundaries based on the termination condition of the while loop

因为数组 `nums`是有序的，所以应该先对 `nums`做预处理，若 `target`小于 `nums`的第一个值或者 `target`大于 `nums`的最后一个值，直接返回-1，不需要进行搜索

需要注意的是，在搜索时应根据while的终止条件来判断更新左右边界时是否需要加减1

Java

```java
class Solution {
    public int search(int[] nums, int target) {
        if (target < nums[0] || target > nums[nums.length - 1]){
            return -1;
        }

        int left = 0;
        int right = nums.length - 1;
        int middle = 0;

        while (left <= right){
            middle = left + ((right - left) >> 2);
            if (target > nums[middle]) left = middle + 1;
            else if (target < nums[middle]) right = middle - 1;
            else return middle;
        }

        return -1;
    }
}
```

Python

```python
class Solution:
    def search(self, nums: List[int], target: int) -> int:
        if target < nums[0] or target > nums[-1]:
            return -1

        left = 0
        right = len(nums) - 1
        middle = 0

        while left <= right:
            middle = left + (right - left) // 2
            if nums[middle] > target:
                right = middle - 1
            elif nums[middle] < target:
                left = middle + 1
            else:
                return middle

        return -1
```
