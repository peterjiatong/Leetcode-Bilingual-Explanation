# Find First and Last Position of Element in Sorted Array / 在排序数组中查找元素的第一个和最后一个位置

Leetcode: https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/

中文力扣：https://leetcode.cn/problems/find-first-and-last-position-of-element-in-sorted-array/

## Description / 题目描述

Given an array of integers `nums` sorted in non-decreasing order, find the starting and ending position of a given `target` value.

If `target` is not found in the array, return `[-1, -1]`.

You must write an algorithm with `O(log n)` runtime complexity.

给你一个按照非递减顺序排列的整数数组 `nums`，和一个目标值 `target`。请你找出给定目标值在数组中的开始位置和结束位置。

如果数组中不存在目标值 `target`，返回 `[-1, -1]`。

你必须设计并实现时间复杂度为 `O(log n)` 的算法解决此问题。

## Constraints **/ 提示**

* `0 <= nums.length <= 10^5`
* `-10^9 <= nums[i] <= 10^9`
* `nums` is a non-decreasing array. / `nums`是一个非递减数组
* `-10^9 <= target <= 10^9`

## Solution: Binary Search / 二分搜索

The basic idea of this problem is similar to a standard binary search. Based on modular programming thinking, we can use two variants of binary search to find the first and last positions of the target element separately.

It's worth mentioning that after obtaining the result of the first position of the target element, we can first check if the target exists in the array. If it doesn't exist, we can directly return `[-1, -1]`. If it does exist, when looking for the last position of the target element, we don't need to search the entire array; we only need to search the portion of the array after the first position of the target.

Each binary search has a time complexity of `O(log n)`, so the time complexity of this algorithm is `O(log n)`.

本题的基本思路与普通的二分搜索近似，基于模块化编程的思维，我们可以将查找元素 `target`的第一个位置和查找元素 `target`的最后一个位置分别各使用一个二分搜索的变种来实现

值得一提的是，在找元素 `target`的第一个位置的结果返回后，我们可以先判断数组中是否存在 `target`，如果不存在，那可以直接返回 `[-1, -1]`，如果存在的话，在查找元素target最后一个位置时，我们就不需要查找整个数组了，只需要寻找数组在 `target`的第一个位置之后的部分就可以了

每一个二分搜索的时间复杂度均为 `O(log n)`，故此算法时间复杂度为 `O(log n)`

```java
class Solution {
    public int[] searchRange(int[] nums, int target) {
        if (nums == null || nums.length == 0) return new int[] {-1, -1};
        int left = findLeft(nums, target);
	// Check edge case
        if (left == -1) return new int[] {-1, -1};
        int right = findRight(nums, left, target);
        return new int[] {left, right};
    }

    private int findLeft(int[] nums, int target){
        int left = 0;
        int right = nums.length - 1;
        int mid = 0;

        while(left + 1 < right){
            mid = left + (right - left) / 2;
            if (nums[mid] >= target) right = mid;
            else left = mid;
        }
	// Post processing
        if (nums[left] == target) return left;
        if (nums[right] == target) return right;
        return -1;
    }

    private int findRight(int[] nums, int leftIndex, int target){
        int left = leftIndex;
        int right = nums.length - 1;
        int mid = 0;

        while(left + 1 < right){
            mid = left + (right - left) / 2;
            if (nums[mid] > target) right = mid;
            else left = mid;
        }
	// Post processing, make sure to check right first
        if (nums[right] == target) return right;
        if (nums[left] == target) return left;
        return -1;
    }
}
```

```python
class Solution:
    def searchRange(self, nums: List[int], target: int) -> List[int]:
        def findLeft(nums, target):
            left = 0
            right = len(nums) - 1
            mid = 0

            while left + 1 < right:
                mid = left + (right - left) // 2
                if nums[mid] >= target:
                    right = mid
                else:
                    left = mid
            # Post processing
            if nums[left] == target:
                return left
            if nums[right] == target:
                return right
            return -1

        def findRight(nums, leftIndex, target):
            left = leftIndex
            right = len(nums) - 1
            mid = 0

            while left + 1 < right:
                mid = left + (right - left) // 2
                if nums[mid] > target:
                    right = mid
                else:
                    left = mid
	    # Post processing, make sure to check right first
            if nums[right] == target:
                return right
            if nums[left] == target:
                return left

        if nums is None or len(nums) == 0:
            return [-1, -1]
        left = findLeft(nums, target) # Check edge case
        if left == -1:
            return [-1, -1]
        right = findRight(nums, left, target)

        return [left, right]
```
