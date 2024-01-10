# Search in Rotated Sorted Array / 搜索旋转排序数组

Leetcode: https://leetcode.com/problems/search-in-rotated-sorted-array

中文力扣: https://leetcode.cn/problems/search-in-rotated-sorted-array

## Description / 题目描述

There is an integer array `nums` sorted in ascending order (with **distinct** values).

Prior to being passed to your function, `nums` is **possibly rotated** at an unknown pivot index `k` (`1 <= k < nums.length`) such that the resulting array is `[nums[k], nums[k+1], ..., nums[n-1], nums[0], nums[1], ..., nums[k-1]]` ( **0-indexed** ). For example, `[0,1,2,4,5,6,7]` might be rotated at pivot index `3` and become `[4,5,6,7,0,1,2]`.

Given the array `nums` **after** the possible rotation and an integer `target`, return *the index of *`target`* if it is in `nums` *, or  `-1`* if it is not in `nums`.

You must write an algorithm with `O(log n)` runtime complexity.

整数数组 `nums` 按升序排列，数组中的值 **互不相同** 。

在传递给函数之前，`nums` 在预先未知的某个下标 `k`（`0 <= k < nums.length`）上进行了  **旋转** ，使数组变为 `[nums[k], nums[k+1], ..., nums[n-1], nums[0], nums[1], ..., nums[k-1]]`（下标 **从 0 开始** 计数）。例如， `[0,1,2,4,5,6,7]` 在下标 `3` 处经旋转后可能变为 `[4,5,6,7,0,1,2]` 。

给你 **旋转后** 的数组 `nums` 和一个整数 `target` ，如果 `nums` 中存在这个目标值 `target` ，则返回它的下标，否则返回 `-1` 。

你必须设计一个时间复杂度为 `O(log n)` 的算法解决此问题。

## **Solution 1: Binary Search / 二分搜索**

This problem will use a modified binary search, as the given array is sorted and then rotated at an unknown point. Thus, for any index, one side of it must be ordered, and the other side maybe disordered.

During the binary search process, we may encounter several cases:

1. `nums[mid] == target`: The answer is found, return `mid`.
2. If `nums[left] < nums[mid]`: This indicates the interval `[left, mid]` is sorted, while the interval `[mid, right]` is disordered (e.g., `[3, 4, 5, 1, 2]`).
   1. If `nums[left] <= target < nums[mid]`, it means the target is in the sorted interval, so we update `right = mid - 1`.
   2. Otherwise, the target is in the disordered interval, so we update `left = mid + 1`.
3. If `nums[left] > nums[mid]`: This indicates the interval `[left, mid]` is disordered, while the interval `[mid, right]` is sorted (e.g., `[4, 5, 1, 2, 3]`).
   1. If `nums[mid] < target <= nums[right]`, it means the target is in the sorted interval, so we update `left = mid + 1`.
   2. Otherwise, the target is in the disordered interval, so we update `right = mid - 1`.

note that this solution also works on any sorted list.

The time complexity of this algorithm is `O(log n)`.

本题将使用一个变种二分搜索，因为本题将给定升序数组在未知的位置旋转了一次，所以在任意元素的左边或右边必然有一边是排序好的，而另一边也许是被打乱顺序的。

在二分搜索的过程中，可能会遇到几种情况：

1. `nums[mid] == target`: 找到答案，返回 `mid`
2. 若`nums[left] < nums[mid]`: 则说明`[left, mid]`这个区间是升序的，而`[mid, right]`的区间是乱序的(如`[3, 4, 5, 1, 2]`)

   1. 此时，若`nums[left] < target < nums[mid]`, 则说明`target`在升序区间，更新`right = mid - 1`
   2. 反之，说明`target`在无序区间，更新`left = mid + 1`
3. 若`nums[left] > nums[mid]`: 则说明`[left, mid]`这个区间是乱序的，而`[mid, right]`的区间是升序的(如`[4, 5, 1, 2, 3]`)

   1. 此时，若`nums[mid] < target < nums[right]`, 则说明`target`在升序区间，更新`left = mid + 1`
   2. 反之，说明`target`在无序区间，更新`right = mid + 1`

本解法在排序好的数组中也能求解

此算法时间复杂度为 `O(log n)`

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

            if nums[left] <= nums[mid]: # [left, mid] is sorted
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

This solution is simpler and more straightforward compared to Solution 1. First, we use binary search to find the pivot point, which is the index where the array was rotated:

1. When `nums[mid] > nums[-1]`: update `left = mid + 1`.
2. Otherwise, update `right = mid - 1`.

After this step, `nums[left]` will be the pivot point. Thus, `[0, left - 1]` is in ascending order and `[left, nums.length - 1]` is also in ascending order, and with the fact `nums[left] < nums[0]`.

Note that if `left = 0`, it implies that `nums` is already sorted in ascending order, and a regular binary search can be performed directly.

Next, compare the `target` with `nums[0]`. If `nums[0] > target`, perform binary search within the interval `[left, nums.length - 1]`. If `nums[0] < target`, binary search should be performed within the interval `[0, left - 1]`.

The time complexity of this algorithm is also `O(log n)`, but since this method uses two binary searches, it is certainly slower than Solution 1 (2 * `O(log n)`).

此解法相较于解法1更加简单直接，首先用二分搜索找到轴点，即数组旋转的下标：

1. 当 `nums[mid] > nums[-1]`时：更新 `left = mid + 1`
2. 反之，更新 `right = mid - 1`

此步骤完成后，`nums[left]`就是轴点，即 `[0, left - 1]`是升序的，`[left, nums.length - 1]`也是升序的，且 `nums[left] < nums[0]`

需要注意的是，若此时 `left = 0`， 证明 `nums`本身就是升序的，直接进行正常的二分搜索即可

之后，比较 `target`和 `nums[0]`的值，若 `nums[0] > target`, 我们就在 `[left, nums.length - 1]`这个区间进行二分搜索，若`nums[0] < target`，则需要在 `[0, left - 1]`这个区间进行二分搜索。

此算法的时间复杂度同为O(log n), 但此算法使用了两个二分搜索，所以一定比解法一慢(2 * O(log n))

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
