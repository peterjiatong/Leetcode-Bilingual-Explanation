# Search in Rotated Sorted Array II / 搜索旋转排序数组 II

Leetcode: https://leetcode.com/problems/search-in-rotated-sorted-array-ii

中文力扣：https://leetcode.cn/problems/search-in-rotated-sorted-array-ii

## Description / 题目描述

There is an integer array `nums` sorted in non-decreasing order (not necessarily with **distinct** values).

Before being passed to your function, `nums` is **rotated** at an unknown pivot index `k` (`0 <= k < nums.length`) such that the resulting array is `[nums[k], nums[k+1], ..., nums[n-1], nums[0], nums[1], ..., nums[k-1]]` ( **0-indexed** ). For example, `[0,1,2,4,4,4,5,6,6,7]` might be rotated at pivot index `5` and become `[4,5,6,6,7,0,1,2,4,4]`.

Given the array `nums` **after** the rotation and an integer `target`, return `true`* if *`target`* is in *`nums`*, or *`false`* if it is not in *`nums`*.*

You must decrease the overall operation steps as much as possible.

已知存在一个按非降序排列的整数数组 `nums` ，数组中的值不必互不相同。

在传递给函数之前，`nums` 在预先未知的某个下标 `k`（`0 <= k < nums.length`）上进行了  **旋转 ** ，使数组变为 `[nums[k], nums[k+1], ..., nums[n-1], nums[0], nums[1], ..., nums[k-1]]`（下标 **从 0 开始** 计数）。例如， `[0,1,2,4,4,4,5,6,6,7]` 在下标 `5` 处经旋转后可能变为 `[4,5,6,6,7,0,1,2,4,4]` 。

给你 **旋转后** 的数组 `nums` 和一个整数 `target` ，请你编写一个函数来判断给定的目标值是否存在于数组中。如果 `nums` 中存在这个目标值 `target` ，则返回 `true` ，否则返回 `false` 。

你必须尽可能减少整个操作步骤。

## Constraints **/ 提示**

* `1 <= nums.length <= 5000`
* `-10^4 <= nums[i] <= 10^4`
* `nums` is guaranteed to be rotated at some pivot. / 题目数据保证 `nums` 在预先未知的某个下标上进行了旋转
* `-10^4 <= target <= 10^4`

## Solution 1: Binary Search / 二分搜索

This problem is essentially the same as LeetCode's Problem 33 [Search in Rotated Sorted Array](https://chatgpt.com/Solution/0033_Search_in_Rotated_Sorted_Array.md). It is strongly recommended to solve Problem 33 first before tackling this one.

In this problem, the given ascending array is rotated at an unknown position, meaning that either the left or right side of any element must be sorted, while the other side **might** be unsorted. This implies that even if we find the value at the middle position of the current array, we cannot determine which boundary to update simply by comparing the value of `target` with the middle position value.

Therefore, we will use a variant of binary search. Since we cannot determine if `target` exists in the **possibly** unsorted section, we must check if `target` exists in the sorted section each time we need to update the boundaries.

Additionally, since the array might contain duplicate values, we should also check if the current boundaries can be ignored before updating them.

During the binary search, we may encounter several scenarios:

1. `nums[mid] == target`: We have found the answer, return `mid`.
2. If the current left and right boundary values are equal to the middle value, since we already know the middle value is not the answer, we also know neither are the left and right boundaries. We can update the boundaries by `left++, right--`. Note that after each update, we need to recalculate the middle index.
3. If `nums[left] < nums[mid]`: This indicates that the interval `[left, mid]` is in ascending order, while the interval `[mid, right]` **might be** unsorted (e.g., `[3, 4, 5, 1, 2]`).
   1. If `nums[left] < target < nums[mid]`, it means `target` is in the ascending interval. Update `right = mid - 1`.
   2. Otherwise, `target` is on the other side. Update `left = mid + 1`.
4. If `nums[left] > nums[mid]`: This indicates that the interval `[left, mid]` is unsorted, while the interval `[mid, right]` **might be** in ascending order (e.g., `[4, 5, 1, 2, 3]`).
   1. If `nums[mid] < target < nums[right]`, it means `target` is in the ascending interval. Update `left = mid + 1`.
   2. Otherwise, `target` is on the other side. Update `right = mid + 1`.

This solution can also solve for sorted arrays, and the time complexity of this algorithm is `O(log n)`.

本题目与力扣第33题[搜索旋转排序数组](/Solution/0033_Search_in_Rotated_Sorted_Array.md)解法基本一致，强烈建议先做完第33题再来思考本题

本题将给定升序数组在未知的位置旋转了一次，说明在任意元素的左边或右边必然有一边是排序好的，而另一边**也许**是被打乱顺序的，也就是说，即便我们找到当前数组的中间位置的值，也无法仅仅通过比较 `target`的值和中间位置的值来确认应该更新哪一个边界

因此我们将使用一个二分搜索的变种，因为我们无法判断 `target`是否存在于**有可能是**乱序的区间，所以每次在需要更新左右边界时，我们要提前判断 `target`是否存在于有序的区间

又因数组中有可能存在重复的值，所以在更新左右边界之前，我们也应该判断当前的左右边界是否可以被忽略

 在二分搜索的过程中，可能会遇到几种情况：

1. `nums[mid] == target`: 找到答案，返回 `mid`
2. 此时我们已知中间的值一定不是答案，如果当前左右边界的值和中间的值相等，说明左右边界也一定不是答案，我们可以更新左右边界 `left++, right--`，需要注意的是，每次更新完左右边界后都要重新计算中间值的下标
3. 若 `nums[left] < nums[mid]`: 则说明 `[left, mid]`这个区间是升序的，而 `[mid, right]`的区间**有可能是**乱序的(如 `[3, 4, 5, 1, 2]`)

   1. 此时，若 `nums[left] < target < nums[mid]`, 则说明 `target`在升序区间，更新 `right = mid - 1`
   2. 反之，说明 `target`在另一边，更新 `left = mid + 1`
4. 若 `nums[left] > nums[mid]`: 则说明 `[left, mid]`这个区间是乱序的，而 `[mid, right]`的区间**有可能是**升序的(如 `[4, 5, 1, 2, 3]`)

   1. 此时，若 `nums[mid] < target < nums[right]`, 则说明 `target`在升序区间，更新 `left = mid + 1`
   2. 反之，说明 `target`在另一边，更新 `right = mid + 1`

本解法在排序好的数组中也能求解， 此算法时间复杂度为 `O(log n)`

Java

```java
class Solution {
    public boolean search(int[] nums, int target) {
        int left = 0;
        int right = nums.length - 1;

        while (left <= right) {
            int mid = left + (right - left) / 2;
            if (nums[mid] == target) return true;
	    else if (nums[left] == nums[mid] && nums[mid] == nums[right]) { // Check duplicates
                left++;
                right--;
            } else if (nums[left] <= nums[mid]){ // [left, mid] is sorted
                if (nums[left] <= target && target < nums[mid]) right = mid - 1;
                else left = mid + 1;
            }else { // [mid, right] is sorted
                if (nums[mid] < target && target <= nums[right]) left = mid + 1;
                else right = mid - 1;  
            }
        }
        return false;
    }
}
```

Python

```python
class Solution:
    def search(self, nums: List[int], target: int) -> bool:
        left = 0
        right = len(nums) - 1

        while left <= right:
            mid = (left + right) // 2

            if nums[mid] == target:
                return True
            elif nums[left] == nums[mid] and nums[mid] == nums[right]: # Check duplicates
                left += 1
                right -= 1
            elif nums[left] <= nums[mid]: # [left, mid] is sorted
                if nums[left] <= target < nums[mid]:
                    right = mid - 1
                else:
                    left = mid + 1
            else: # [mid, right] is sorted
                if nums[mid] < target <= nums[right]:
                    left = mid + 1
                else:
                    right = mid - 1

        return False
```
