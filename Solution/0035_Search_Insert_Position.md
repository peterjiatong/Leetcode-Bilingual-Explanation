# Search Insert Position /搜索插入位置

Leetcode: https://leetcode.com/problems/search-insert-position/

中文力扣：https://leetcode.cn/problems/search-insert-position/

## Description / 题目描述

Given a sorted array of distinct integers and a target value, return the index if the target is found. If not, return the index where it would be if it were inserted in order.

You must write an algorithm with `O(log n)` runtime complexity.

给定一个排序数组和一个目标值，在数组中找到目标值，并返回其索引。如果目标值不存在于数组中，返回它将会被按顺序插入的位置。

请必须使用时间复杂度为 `O(log n)` 的算法。

## Solution: Binary Search / 二分搜索

When performing a binary search on the given array `nums`, there are three possible scenarios during the search:

1. If `nums[mid] == target`, return `mid`.
2. If `nums[mid] > target`, update `right = mid`.
3. If `nums[mid] < target`, update `left = mid`.

When `left + 1` is not less than `right` (when left and right are adjacent), end the search. At this point, neither `left` nor `right` has been checked:

1. If `nums[left] >= target`, return `left`.
2. If `nums[right] >= target`, return `right`.
3. If none of the above conditions are met, it means that `target` is greater than `right`, so return `right + 1`.

The time complexity of this algorithm is O(log n).

对给定数组 `nums`进行二分搜索，搜索途中，有以下三种可能性：

1. 若 `nums[mid] == target`, 返回 `mid`
2. 若 `nums[mid] > target`, 则更新 `right = mid`
3. 若 `nums[mid] < target`, 则更新 `left = mid`

当 `left + 1` 不小于 `right`时(当左右相邻时)，结束搜索，此时，left和right本身还为被检查过：

1. 若 `nums[left] >= target` 返回 `left`
2. 若 `(nums[right] >= target) `返回 ` right`
3. 若以上均不满足，说明 `target`大于 `right`，返回 `right + 1`

此算法时间复杂度为O(log n)

Java

```java
class Solution {
    public int searchInsert(int[] nums, int target) {
        int left = 0;
        int right = nums.length - 1;

        while(left + 1 < right){
            int mid = left + (right - left) / 2;
            if (nums[mid] == target) return mid;
            else if (nums[mid] > target) right = mid;
            else left = mid;
        }

        if (nums[left] >= target) return left;
        if (nums[right] >= target) return right;
        return right + 1;
    }
}

```

Python

```python
class Solution:
    def searchInsert(self, nums: List[int], target: int) -> int:
        left = 0
        right = len(nums) - 1

        while left + 1 < right:
            mid = left + (right - left) // 2
            if nums[mid] == target:
                return mid
            elif nums[mid] > target:
                right = mid
            else:
                left = mid
        
        if nums[left] >= target:
            return left
        elif nums[right] >= target:
            return right
        return right + 1
      
```
