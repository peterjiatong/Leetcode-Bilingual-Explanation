# Rotate Array / 轮转数组

Leetcode: https://leetcode.com/problems/rotate-array/

中文力扣: https://leetcode.cn/problems/rotate-array/

## Description / 题目描述

Given an integer array `nums`, rotate the array to the right by `k` steps, where `k` is non-negative.

给定一个整数数组 `nums`，将数组中的元素向右轮转 `k` 个位置，其中 `k` 是非负数。

## Solution 1: Reversing / 翻转法

We first take the modulo of `k` with `n` to get an effective step count `k`. Then, we perform three reverse operations on the given array `nums`:

1. Reverse the entire array.
2. Reverse the first `k` elements of the array.
3. Finally, reverse the remaining elements of the array.

This approach has a time complexity of `O(n)`, because we do not use additional space, meeting the follow-up requirement of an in-place algorithm with `O(1)` space complexity.

我们将k对n取模得到有效的步数k，之后我们对给定数组nums进行三次翻转：

1. 先将整个数组翻转
2. 接着翻转数组的前 `k` 个元素。
3. 最后翻转数组中剩余的元素。

此方法时间复杂度为 `O(n)`。因为我们并没有使用额外的空间，故满足进阶要求中的原地算法的`O(1)`空间复杂度要求

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
