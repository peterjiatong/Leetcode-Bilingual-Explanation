# Search in Rotated Sorted Array / 搜索旋转排序数组

Leetcode: https://leetcode.com/problems/search-in-rotated-sorted-array

中文力扣: https://leetcode.cn/problems/search-in-rotated-sorted-array

## Description / 题目描述

There is an integer array `nums` sorted in ascending order (with **distinct** values).

Prior to being passed to your function, `nums` is **possibly rotated** at an unknown pivot index `k` (`1 <= k < nums.length`) such that the resulting array is `[nums[k], nums[k+1], ..., nums[n-1], nums[0], nums[1], ..., nums[k-1]]` ( **0-indexed** ). For example, `[0,1,2,4,5,6,7]` might be rotated at pivot index `3` and become `[4,5,6,7,0,1,2]`.

Given the array `nums` **after** the possible rotation and an integer `target`, return _the index of _`target`_ if it is in `nums` _, or `-1`\* if it is not in `nums`.

You must write an algorithm with `O(log n)` runtime complexity.

整数数组 `nums` 按升序排列，数组中的值 **互不相同** 。

在传递给函数之前，`nums` 在预先未知的某个下标 `k`（`0 <= k < nums.length`）上进行了 **旋转** ，使数组变为 `[nums[k], nums[k+1], ..., nums[n-1], nums[0], nums[1], ..., nums[k-1]]`（下标 **从 0 开始** 计数）。例如， `[0,1,2,4,5,6,7]` 在下标 `3` 处经旋转后可能变为 `[4,5,6,7,0,1,2]` 。

给你 **旋转后** 的数组 `nums` 和一个整数 `target` ，如果 `nums` 中存在这个目标值 `target` ，则返回它的下标，否则返回 `-1` 。

你必须设计一个时间复杂度为 `O(log n)` 的算法解决此问题。

## Constraints **/ 提示**

- `1 <= nums.length <= 5000`
- `-10^4 <= nums[i] <= 10^4`
- All values of `nums` are **unique**. / `nums` 中的每个值都 **独一无二**
- `nums` is an ascending array that is possibly rotated. / 题目数据保证 `nums` 在预先未知的某个下标上进行了旋转
- `-10^4<= target <= 10^4`

## **Solution 1: Binary Search / 二分搜索**

The problem involves a given ascending array that has been rotated once at an unknown position. which on either side of any element, one side must be sorted, while the other side **may be** unsorted. This means that even if we find the middle value of the current array, we cannot determine which boundary to update by simply comparing the `target` value with the middle value.

Therefore, we will use a variant of binary search. Since we cannot determine if `target` is in the possibly unsorted segment, we must check if `target` is in the sorted segment each time when we need to update the left or right boundary.

During the binary search, we may encounter several situations:

1. `nums[mid] == target`: If the middle element is the target, return `mid`.
2. If `nums[left] <= nums[mid]`: It means the `[left, mid]` segment is sorted, while the `(mid, right]` segment **may be** unsorted (e.g., `[3, 4, 5, 1, 2]`).
   1. If `nums[left] <= target < nums[mid]`, it means `target` is in the sorted segment, so update `right = mid - 1`.
   2. Otherwise (`nums[mid] < target <= nums[right]`), it means `target` is in the other segment, so update `left = mid + 1`.
3. If `nums[left] > nums[mid]`: It means the `[left, mid]` segment is unsorted, while the `(mid, right]` segment **may be** sorted (e.g., `[4, 5, 1, 2, 3]`).
   1. If `nums[mid] < target <= nums[right]`, it means `target` is in the sorted segment, so update `left = mid + 1`.
   2. Otherwise (`nums[left] <= target < nums[mid]`), it means `target` is in the other segment, so update `right = mid - 1`.

This solution can also handle a normally sorted array. The time complexity of this algorithm is `O(log n)`.

本题将给定升序数组在未知的位置旋转了一次，说明在任意元素的左边或右边必然有一边是排序好的，而另一边**也许**是被打乱顺序的，也就是说，即便我们找到当前数组的中间位置的值，也无法仅仅通过比较 `target`的值和中间位置的值来确认应该更新哪一个边界

因此我们将使用一个二分搜索的变种，因为我们无法判断 `target`是否存在于**有可能是**乱序的区间，所以每次在需要更新左右边界时，我们要提前判断 `target`是否存在于有序的区间

在二分搜索的过程中，可能会遇到几种情况：

1. `nums[mid] == target`: 找到答案，返回 `mid`
2. 若 `nums[left] <= nums[mid]`: 则说明 `[left, mid]`这个区间是升序的，而 `(mid, right]`的区间**有可能是**乱序的(如 `[3, 4, 5, 1, 2]`)

   1. 此时，若 `nums[left] < target < nums[mid]`, 则说明 `target`在升序区间，更新 `right = mid - 1`
   2. 反之 (`nums[mid] < target <= nums[right]`)，说明 `target`在另一边，更新 `left = mid + 1`

3. 若 `nums[left] > nums[mid]`: 则说明 `[left, mid]`这个区间是乱序的，而 `(mid, right]`的区间**有可能是**升序的(如 `[4, 5, 1, 2, 3]`)

   1. 此时，若 `nums[mid] < target <= nums[right]`, 则说明 `target`在升序区间，更新 `left = mid + 1`
   2. 反之 (`nums[left] <= target < nums[mid]`)，说明 `target`在另一边，更新 `right = mid + 1`

本解法在排序好的数组中也能求解， 此算法时间复杂度为 `O(log n)`

Java

```java
class Solution {
    public int search(int[] nums, int target) {
        int left = 0;
        int right = nums.length - 1;

        while (left <= right) {
            int mid = left + (right - left) / 2;
            if (nums[mid] == target) return mid;
            else if (nums[left] <= nums[mid]){ // [left, mid] is sorted
                if (nums[left] <= target && target < nums[mid]) right = mid - 1;
                else left = mid + 1;
            }else { // [mid, right] is sorted
                if (nums[mid] < target && target <= nums[right]) left = mid + 1;
                else right = mid - 1;
            }
        }
        return -1;
    }
}

```

Python

```python
class Solution:
    def search(self, nums: List[int], target: int) -> int:
        left = 0
        right = len(nums) - 1

        while left <= right:
            mid = (left + right) // 2

            if nums[mid] == target:
                return mid
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

        return -1

```

## Solution 2: Find Pivot + Binary Search / 找轴点 + 二分搜索

The problem involves a given ascending array that has been rotated once at an unknown position. If the rotated array is not already in ascending order (i.e., rotated at index 0, meaning the array remains unchanged), there must exist a pivot point `p` such that the value of pivot point is greater than the value of its neighbors (`nums[p - 1] < nums[p] > nums[p + 1]`). This means the segment `[0, p]` is sorted in ascending order, and the segment `[p + 1, nums.length - 1]` is also sorted in ascending order, with `nums[p + 1] < nums[0]`.

First, we use binary search to find the pivot point. while the left boundary does not exceed the right boundary (left <= right):

1. If `nums[mid] > nums[-1]`, update `left = mid + 1`.
2. Otherwise, update `right = mid - 1`.

After the binary search, `left` will be the value to the right of pivot point, `nums[p + 1]` (note that if `left = 0` at this point, it means `nums` itself is in ascending order, so we can proceed with a normal binary search).

Next, compare `target` with `nums[0]`. If `nums[0] >= target`, we perform binary search in the segment `[left, nums.length - 1]` (since `nums[p + 1]` must be less than `nums[0]`). If `nums[0] < target`, we perform binary search in the segment `[0, left - 1]`.

The time complexity of this algorithm is also `O(log n)`. However, since this algorithm uses two binary searches, it must be slower than the previous solution.

本题将给定升序数组在未知的位置旋转了一次，说明旋转过的数组若非本身就是升序(在下标 0 处旋转，即数组没有变化)，就一定存在一个轴点 `p`，满足轴点的值大于轴点左右两边的值(`nums[p - 1] < nums[p] > num[p + 1]`)，即 `[0, p]`是升序的，`[p + 1, nums.length - 1]`也是升序的，且 `nums[p + 1] < nums[0]`

首先用二分搜索找到轴点，当左右边界没有越过时(left <= right)：

1. 当 `nums[mid] > nums[-1]` 时：更新 `left = mid + 1`
2. 反之，更新 `right = mid - 1`

二分搜索后， `left`就是我们要找的轴点的下一个值, `nums[p + 1]` (需要注意的是，若此时 `left = 0`， 证明 `nums` 本身就是升序的，直接进行正常的二分搜索即可)

之后，比较 `target`和 `nums[0]`的值，如果 `nums[0] >= target`, 我们就在 `[left, nums.length - 1]`这个区间进行二分搜索(因为 `nums[p + 1]` 一定小于 `nums[0]`)，如果 `nums[0] < target`，则需要在 `[0, left - 1]`这个区间进行二分搜索。

此算法的时间复杂度同为 `O(log n)`, 但此算法使用了两个二分搜索，所以一定比上一个解法慢

Java

```java
class Solution {
    public int search(int[] nums, int target) {
        int left = 0;
        int right = nums.length - 1;
        int rightNum = nums[nums.length - 1];

        while (left <= right) {
            int mid = left + (right - left) / 2;
            if (nums[mid] > rightNum) {
                left = mid + 1;
            } else {
                right = mid - 1;
            }
        }

        if (left == 0){
            right = nums.length - 1;
        }else if (nums[0] > target){
            right = nums.length - 1;
        }else {
            right = left - 1;
            left = 0;
        }

        while (left <= right) {
            int mid = (left + right) / 2;
            if (nums[mid] == target) return mid;
            else if (nums[mid] > target) right = mid - 1;
            else left = mid + 1;
        }
        return -1;
    }
}

```

Python

```python
class Solution:
    def search(self, nums: List[int], target: int) -> int:
        left = 0
        right = len(nums) - 1
        rightNum = nums[-1]

        while left <= right:
            mid = left + (right - left) // 2
            if (nums[mid] > rightNum):
                left = mid + 1
            else:
                right = mid - 1

        if left == 0:
            right = len(nums) - 1
        elif nums[0] > target:
            right = len(nums) - 1
        else:
            right = left - 1
            left = 0

        while left <= right:
            mid = left + (right - left)
            if nums[mid] == target:
                return mid
            elif nums[mid] > target:
                right = mid - 1
            else:
                left = mid + 1

        return -1

```
