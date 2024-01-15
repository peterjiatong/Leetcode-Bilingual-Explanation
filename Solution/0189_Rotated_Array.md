# Rotate Array / 轮转数组

Leetcode: https://leetcode.com/problems/rotate-array/

中文力扣: https://leetcode.cn/problems/rotate-array/

## Description / 题目描述

Given an integer array `nums`, rotate the array to the right by `k` steps, where `k` is non-negative.

给定一个整数数组 `nums`，将数组中的元素向右轮转 `k` 个位置，其中 `k` 是非负数。

## Solution 1: Reversing / 翻转法

We first calculate the effective rotation amount `k` by taking the remainder of `k` when divided by the array's length. And we can reverse all elements of the array first. And then reverse the first `k` element of the array. Last, we reverse the rest `n - k` elements in the array.

The time complexity of this solution is `O(n)`.

我们首先通过取 `k` 除以数组长度的余数来计算有效的旋转量 `k`。然后，我们先反转数组中的所有元素。接着反转数组的前 `k` 个元素。最后，我们反转数组中剩余的 `n - k` 个元素。

此方法时间复杂度为 `O(n)`。

Java:

```java
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

```python
class Solution:
    def rotate(self, nums: List[int], k: int) -> None:
        k %= len(nums)
        nums[:] = nums[-k:] + nums[:-k] # Python treat this line of code as the method we discussed above
```

## Solution 2: Extra Space / 额外空间

This solution uses extra space, which is not the recommended approach.

First, create a new empty array `temp` with the same length as `nums`. Then, iterate through `nums` and update `temp[(i + k) % nums.length]` to be `nums[i]`. After Iteration, copy the elements from `temp` back to `nums`.

The time complexity of this algorithm is `O(n)`, but the space complexity is also `O(n)`.

此解法使用额外空间，不是我们推荐的解法

首先创建一个与 `nums`长度相同的新数组 `temp`，遍历 `nums`，更新 `temp[(i + k) % nums.length]` 为 `nums[i]`，遍历完成后，将 `temp`中的元素复制回 `nums`中

此算法时间复杂度为`O(n)`，但空间复杂度亦为`O(n)`

Java

```java
class Solution {
    public void rotate(int[] nums, int k) {
        int n = nums.length;
        int[] temp = new int[n];
        for (int i = 0; i < n; i++){
            temp[(i + k) % n] = nums[i];
        }

        for (int i = 0; i < n; i++){
            nums[i] = temp[i];
        }
    }
}
```

Python

```python
class Solution:
    def rotate(self, nums: List[int], k: int) -> None:
        n = len(nums)
        temp = [None] * n
    
        for i in range(n):
            temp[(i+k)% n] = nums[i]

        for i in range(n):
            nums[i] = temp[i]
    
```
