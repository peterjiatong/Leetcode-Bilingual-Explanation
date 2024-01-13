# Rotate Array / 轮转数组

Leetcode: https://leetcode.com/problems/rotate-array/

中文力扣: https://leetcode.cn/problems/rotate-array/

## Description / 题目描述

Given an integer array `nums`, rotate the array to the right by `k` steps, where `k` is non-negative.

给定一个整数数组 `nums`，将数组中的元素向右轮转 `k` 个位置，其中 `k` 是非负数。

## Solution: Reversing

We first calculate the effective rotation amount `k` by taking the remainder of `k` when divided by the array's length. And we can reverse all elements of the array first. And then reverse the first `k` element of the array. Last, we reverse the rest `n - k` elements in the array.

The time complexity of this solution is `O(n)`.

我们首先通过取 `k` 除以数组长度的余数来计算有效的旋转量 `k`。然后，我们先反转数组中的所有元素。接着反转数组的前 `k` 个元素。最后，我们反转数组中剩余的 `n - k` 个元素。

此方法时间复杂度为 `O(n)`。

Java:

```
class Solution {
    public void rotate(int[] nums, int k) {
        int n = nums.length;
        k = k % n;
        reverse(nums, 0, n - 1);
        reverse(nums, 0, k - 1);
        reverse(nums, k, n - 1);
    }

    private void reverse(int[] nums, int start, int end) {
        while (start < end) {
            int temp = nums[start];
            nums[start]= nums[end];
            nums[end] = temp;
            start++;
            end--;
        }
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
