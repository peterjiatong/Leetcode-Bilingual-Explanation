# Sqrt(x) / x 的平方根 

Leetcode: https://leetcode.com/problems/sqrtx/

中文力扣： https://leetcode.cn/problems/sqrtx/

## Description / 题目描述

Given a non-negative integer `x`, return *the square root of* *`x`  rounded down to the nearest integer* . The returned integer should be **non-negative** as well.

You **must not use** any built-in exponent function or operator.

* For example, do not use `pow(x, 0.5)` in c++ or `x ** 0.5` in python.

给你一个非负整数 `x` ，计算并返回 `x` 的 **算术平方根** 。

由于返回类型是整数，结果只保留  **整数部分** ，小数部分将被 **舍去 。**

 **注意：** 不允许使用任何内置指数函数和算符，例如 `pow(x, 0.5)` 或者 `x ** 0.5` 。

## Solution: Binary Search / 二分搜索

Using binary search to iterate from 2 to x/2, we set the left boundary to 2 because binary search would encounter errors when `x == 0` or `x == 1`. Therefore, we handle these two corner cases before searching. We set the right boundary to x/2 because the square root of x must be less than x/2.

During the search, the following three cases may occur:

1. `mid^2 <= x` and `(mid + 1)^2 > x`: Return `mid`.
2. If the above condition is not met, and `mid^2 < x`: Update `left = mid + 1`.
3. `mid^2 > x`: Update `right = mid - 1`.

Please note: In some languages (like Java), `mid^2` may cause an overflow issue, so it's important to handle the data structure for `mid^2` accordingly. When `x == 2` or `x == 3`, the right boundary is initialized to a value less than the left boundary, so you should return the value of the right boundary at the end.

The time complexity of this algorithm is O(n).

使用二分搜索遍历[2, x/2]，左边界设置为2是因为当 `x == 0` 或 ` x == 1`时，二分搜索将会报错，所以我们在搜索前优先处理这两个边角案例；将右边界设置为x/2是因为 `sqrt(x)`一定小于x/2。

在搜索时，有可能出现一下3种情况：

1. `mid^2 <= x` 且 `(mid + 1)^2 > x`时：返回 `mid`
2. 若不满足上面的条件，且 `mid^2 < x`时：更新 `left = mid + 1`
3. `mid^2 > x` 时：更新 `right  = mid - 1`

请注意：部分语言(如Java)中 `mid^2`会出界，请具体记录 `mid^2`的数据结构；当 `x == 2` 或 `x == 3` 时，右边界会被初始化为小于左左边界的值，所以在最后应该返回右边界的值

此算法时间复杂度为`O(n)`

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
