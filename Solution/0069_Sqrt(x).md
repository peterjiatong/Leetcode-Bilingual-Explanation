# Sqrt(x) / x 的平方根

Leetcode: https://leetcode.com/problems/sqrtx/

中文力扣：https://leetcode.cn/problems/sqrtx/

## Description / 题目描述

Given a non-negative integer `x`, return *the square root of* *`x`  rounded down to the nearest integer* . The returned integer should be **non-negative** as well.

You **must not use** any built-in exponent function or operator.

* For example, do not use `pow(x, 0.5)` in c++ or `x ** 0.5` in python.

给你一个非负整数 `x` ，计算并返回 `x` 的 **算术平方根** 。

由于返回类型是整数，结果只保留  **整数部分** ，小数部分将被 **舍去 。**

 **注意：** 不允许使用任何内置指数函数和算符，例如 `pow(x, 0.5)` 或者 `x ** 0.5` 。

## Constraints **/ 提示**

* `0 <= x <= 2^31 - 1`

## Solution: Binary Search / 二分搜索

In this problem, we use binary search to find the integer square root of a number `x`. We begin by handling corner cases: if `x` equals `0` or `1`, we simply return `x`.

Based on mathematical principles, we know that the square root of `x` is less than or equal to `x/2`. Therefore, we confine our search to the interval `[2, x/2]` using binary search.

During the search process, we consider the following three cases:

1. If `mid^2 <= x` and `(mid + 1)^2 > x`, because the problem specifies rounded down to the nearest integer, `mid` is the integer square root we are looking for.
2. If `mid^2 < x`, update the search range to `left = mid + 1`.
3. If `mid^2 > x`, update the search range to `right = mid - 1`.

It is important to note that in cases where `x == 2` or `x == 3`, initially the right boundary might be less than the left boundary. Therefore, following a defensive programming approach, after completing the binary search, we should return the value of the right boundary as the integer square root.

It's worth mentioning that in some languages (like Java), care should be taken to ensure that `mid^2` does not cause overflow when using data structures.

The time complexity of this algorithm is `O(log x)`.

本题我们将使用二分搜索进行解题，在搜索求解整数 `x` 的平方根时，我们首先处理边界情况：如果 `x` 等于 `0` 或 `1`，直接返回 `x`。

根据数学原理，已知 `x` 的平方根一定小于等于 `x/2`。因此，我们将搜索范围限定在 `[2, x/2]` 区间内进行二分搜索。

在搜索过程中，我们需要考虑以下三种情况：

1. 如果 `mid^2 <= x` 且 `(mid + 1)^2 > x`，因为题目要求返回整数部分结果, 此时 `mid` 即为所求的整数平方根。
2. 如果 `mid^2 < x`，则更新搜索范围为 `left = mid + 1`。
3. 如果 `mid^2 > x`，则更新搜索范围为 `right = mid - 1`。

特别注意，在 `x == 2` 或 `x == 3` 的情况下，初始时右边界可能小于左边界，因此在二分搜索结束后，基于保护性编程的想法，应返回右边界的值作为整数平方根。

值得一提的是，在一些语言中（如Java），在使用数据结构时应注意确保 `mid^2` 不会溢出。

该算法的时间复杂度为 `O(log x)`。

Java

```java
class Solution {
    public int mySqrt(int x) {
        if (x == 0 || x == 1) return x;
  
        int left = 2;
        int right = x / 2;

        while (left <= right){
            int mid = left + (right - left) / 2;
            long midSqr = (long)mid * mid;
            long midPlus1Sqr = (long)(mid + 1) * (mid + 1);
            if (midSqr <= x && midPlus1Sqr > x) return mid;
            else if(midSqr < x) left = mid + 1;
            else right = mid - 1;
        }

        return right; // Edge Case
    }
}

```

Python

```python
class Solution:
    def mySqrt(self, x):
        if (x == 0 or x == 1):
            return x
  
        left = 0
        right = x // 2

        while(left <= right):
            mid = left + (right - left) // 2
            midSqr = mid * mid
            midPlus1Sqr = (mid + 1) * (mid + 1)
            if midSqr <= x < midPlus1Sqr:
                return mid
            elif midSqr < x:
                left = mid + 1
            else:
                right = mid - 1

        return right # Edge case

```
