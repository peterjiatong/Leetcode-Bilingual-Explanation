# Product of Array Except Self / 除自身以外数组的乘积

Leetcode: https://leetcode.com/problems/product-of-array-except-self/

中文力扣：https://leetcode.cn/problems/product-of-array-except-self/

## Description / 题目描述

Given an integer array `nums`, return *an array* `answer` *such that* `answer[i]` *is equal to the product of all the elements of* `nums` *except* `nums[i]`.

The product of any prefix or suffix of `nums` is **guaranteed** to fit in a **32-bit** integer.

You must write an algorithm that runs in `O(n)` time and without using the division operation.

给你一个整数数组 `nums`，返回 *数组 `answer` ，其中 `answer[i]` 等于 `nums` 中除 `nums[i]` 之外其余各元素的乘积* 。

题目数据 **保证** 数组 `nums`之中任意元素的全部前缀元素和后缀的乘积都在  **32 位** 整数范围内。

请  **不要使用除法，** 且在 `O(n)` 时间复杂度内完成此题。

## Solution : Two Side Traverse / 分别从两端遍历

Before solving this problem, let's analyze an example:

Suppose `nums = [1, 2, 3, 4]`, then the output should be `[24, 12, 8, 6]`, which is equivalent to `[2x3x4, 1x3x4, 1x2x4, 1x2x3]`. This can also be interpreted as `[1x2x3x4, 1x1x3x4, 1x2x1x4, 1x2x3x1]`. In other words, to solve this problem, we simply replace the number at index `i` with 1 when calculating the value for index `i`.

However, the challenge requires solving this problem within a time complexity of `O(n)`, so the brute force method is not applicable.

We can solve this problem by traversing the given array from both ends. During each traversal, we update the value at index `i` with the product of all elements before index `i` (if there are no elements before it, the value at index `i` is set to 1). For example, with `[1, 2, 3, 4]`, when updating the value at index 2, traversing from the left gives us 1x2=2, and from the right gives 4. Multiplying the results of both traversals gives us the final result of 8, which is 1x2x4, effectively ignoring the number 3 at index 2.

This solution has a time complexity of `O(n)`.

解决此问题前，我们先分析一个例子：

若`nums` = [1, 2, 3, 4], `b`应该得到[24, 12, 8 , 6], 即[2x3x4, 1x3x4, 1x2x4, 1x2x3], 我们也可以将其视为[1x2x3x4, 1x1x3x4, 1x2x1x4, 1x2x3x1], 换而言之，只要在计算下标`i`时，将处于下标`i`的数变成1，就可以解决此问题

但根据题目要求，需要在 `O(n)` 时间复杂度内完成此题，所以蛮力法并不适用于此题

我们可以分别从两边遍历给定数组来解决此问题，每次遍历时，我们用当前下标 `i`之前的元素的乘积来更新下标 `i`所处的数值(若前面没有元素，则将下标 `i`的值设为1)，例如[1, 2, 3, 4]，更新下标2的数值时，从左遍历就得到1x2 = 2, 从右遍历会得到4，我们将两边遍历的结果相乘，就得到了最终结果8，即1x2x4，忽略了下标2上的数字3

此解法时间复杂度为O(n)

Java:

```java
class Solution {
    public int[] productExceptSelf(int[] nums) {
        int[] ans = new int[nums.length];
        int cur = 1;

        for (int i = 0; i < nums.length; i++){
            ans[i] = cur;
            cur = cur * nums[i];
        }

        cur = 1;
        for (int i = 0; i < nums.length; i++){
            int curIndex = nums.length - 1 - i; // Track the index from right to left
            ans[curIndex] = ans[curIndex] * cur;
            cur = cur * nums[curIndex];
        }

        return ans;
    }
}

```

Python:

```python
class Solution:
    def productExceptSelf(self, nums: List[int]) -> List[int]:
        ans = [0] * len(nums)
        cur = 1
        for i in range(len(nums)):
            ans[i] = cur
            cur = cur * nums[i]

        cur = 1
        for i in range(len(nums)):
            ans[-(i + 1)] = ans[-(i + 1)] * cur # Now ans[i] is the product of part on the left of index i and on the right of index i
            cur = cur * nums[-(i + 1)]

        return ans

```
