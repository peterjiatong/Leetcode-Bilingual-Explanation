# Rotate Array / 轮转数组

Leetcode: https://leetcode.com/problems/rotate-array/

中文力扣: https://leetcode.cn/problems/rotate-array/

## Description / 题目描述

Given an integer array `nums`, rotate the array to the right by `k` steps, where `k` is non-negative.

给定一个整数数组 `nums`，将数组中的元素向右轮转 `k` 个位置，其中 `k` 是非负数。

## Solution: Reversing

We first calculate the effective rotation amount `k` by taking the remainder of `k` when divided by the array's length. And we can reverse the array's first `k` element. And then reverse the remaining element of the array. Last, we switch the two subarrays and assign them back to `nums`.

The time complexity of this solution is `O(n)`

我们首先通过将 `k` 除以数组长度并取余数来计算有效的旋转量 `k`。然后我们可以先反转数组的前 `k` 个元素。接着反转数组的剩余元素。最后，我们交换这两个子数组并将它们重新赋值给 `nums`。

此方法时间复杂度为 `O(n)`

Java:

```
class Solution {
    public void rotate(int[] nums, int k) {
    
    }
}
```

Python:

```
class Solution:
    def rotate(self, nums: List[int], k: int) -> None:
        """
        Do not return anything, modify nums in-place instead.
        """
        k %= len(nums)
        nums[:] = nums[-k:] + nums[:-k]
```
