# [Search in Rotated Sorted Array](https://leetcode.com/problems/search-in-rotated-sorted-array/)

Leetcode: https://leetcode.com/problems/search-in-rotated-sorted-array/

中文力扣: https://leetcode.cn/problems/search-in-rotated-sorted-array/description/

## Description / 题目描述

There is an integer array `nums` sorted in ascending order (with **distinct** values).

Prior to being passed to your function, `nums` is **possibly rotated** at an unknown pivot index `k` (`1 <= k < nums.length`) such that the resulting array is `[nums[k], nums[k+1], ..., nums[n-1], nums[0], nums[1], ..., nums[k-1]]` ( **0-indexed** ). For example, `[0,1,2,4,5,6,7]` might be rotated at pivot index `3` and become `[4,5,6,7,0,1,2]`.

Given the array `nums` **after** the possible rotation and an integer `target`, return *the index of *`target`* if it is in `nums` *, or  `-1`* if it is not in `nums`.

You must write an algorithm with `O(log n)` runtime complexity.

整数数组 `nums` 按升序排列，数组中的值 **互不相同** 。

在传递给函数之前，`nums` 在预先未知的某个下标 `k`（`0 <= k < nums.length`）上进行了  **旋转** ，使数组变为 `[nums[k], nums[k+1], ..., nums[n-1], nums[0], nums[1], ..., nums[k-1]]`（下标 **从 0 开始** 计数）。例如， `[0,1,2,4,5,6,7]` 在下标 `3` 处经旋转后可能变为 `[4,5,6,7,0,1,2]` 。

给你 **旋转后** 的数组 `nums` 和一个整数 `target` ，如果 `nums` 中存在这个目标值 `target` ，则返回它的下标，否则返回 `-1` 。

你必须设计一个时间复杂度为 `O(log n)` 的算法解决此问题。

## **Solution: Binary Search / 二元搜寻法**

The solution using Binary Search to trasverse through the given rotated array `nums`. We will have three labels `left` , `right`, and `mid`. `left` is used to track the beginning of the array, `right` is the end of the array and `mid` is the midpoint of `left` and `right`. We intialize `left` to 0 and `right` to n - 1. As we go throught the array, we can determine if the left part of nums is sorted, by checking if the beginning element is smaller than or equal to midpoint. If so, the left part of nums is sorted, otherwise, the right part has to be sorted.

For example, for a `nums` like `[4,5,6,7,0,1,2]`, `nums[left] = 4, nums[right] = 2, nums[mid] = 7`. Here, the left part of nums is `[4,5,6,7]` which is sorted, but the right part `[7,0,1,2]` is not sorted.

By having sorted half in mind. If the left half is sorted, we can check if `target` is in the left half by comparing target with the beginning of the left half and the midpoint. If target is in the sorted left half, we update `right` to `mid - 1`. Otherwise the target must be in the right half, we update `left` to `mid + 1`.

In the case where the right half is sorted, if `target` is in the sorted right half, we will update `left` to `mid + 1` . Else the target is in the left half. then we will update `right` to `mid - 1`.

With this modified Binary Search, we maintained the `O(log n)` time of Binary Search by determine which half of the array is sorted so that we can use the sorted property to elimate half of the elements in the array by every iteration. The space complexity is `O(1)`because we only used constant amount of variables no matter the size of the array.

Python:

```python
class Solution:
    def search(self, nums: List[int], target: int) -> int:
        left = 0
        right = len(nums) - 1

        while left <= right:
            mid = (left + right) // 2

            if nums[mid] == target:
                return mid

            if nums[left] <= nums[mid]:
                if nums[left] <= target < nums[mid]:
                    right = mid - 1
                else:
                    left = mid + 1
            else:
                if nums[mid] < target <= nums[right]:
                    left = mid + 1
                else:
                    right = mid - 1

        return -1
```
