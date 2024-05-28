# Container With Most Water / 盛最多水的容器

Leetcode: https://leetcode.com/problems/container-with-most-water

中文力扣：https://leetcode.cn/problems/container-with-most-water

## Description / 题目描述

You are given an integer array `height` of length `n`. There are `n` vertical lines drawn such that the two endpoints of the `ith` line are `(i, 0)` and `(i, height[i])`.

Find two lines that together with the x-axis form a container, such that the container contains the most water.

Return  *the maximum amount of water a container can store* .

**Notice** that you may not slant the container.

给定一个长度为 `n` 的整数数组 `height` 。有 `n` 条垂线，第 `i` 条线的两个端点是 `(i, 0)` 和 `(i, height[i])` 。

找出其中的两条线，使得它们与 `x` 轴共同构成的容器可以容纳最多的水。

返回容器可以储存的最大水量。

**说明：** 你不能倾斜容器。

## Solution: Two Pointers / 双指针

The amount of water a container can hold depends on the height of the shorter side of the boundary, so each time, we should update the boundary of the shorter side until the left and right boundaries meet.

Using two pointers `left` and `right` to record the left and right boundaries, respectively, if the current height of the left and right boundaries can store the maximum amount of water, record it.

This algorithm has a time complexity of `O(n)`.

桶中能装多少水取决于更短一侧的边界的高度，所以每次都应该更新较小一侧的边界，直至左右边界重合

使用两个指针 `left`和 `right`，分别记录左右边界，如果当前左右边界的高度可以储存最大水量，将其记录下来

此算法时间复杂度为 `O(n)`

Java:

```java
class Solution {
    public int maxArea(int[] height) {
        int left = 0;
        int right = height.length - 1;
        int max = 0;

        while (left < right){
            int temp = Math.min(height[left], height[right]) * (right - left); # Count current area
            if (temp > max) max = temp;
            if (height[left] > height[right]){
                right --;
            }else {
                left ++;
            }
        }
  
        return max;
    }
}

```

Python:

```python
class Solution:
    def maxArea(self, height: List[int]) -> int:
        left = 0
        right = len(height) - 1
        max = 0

        while left < right:
            temp = min(height[left], height[right]) * (right - left)
            if temp > max: max = temp
            if height[left] > height[right]:
                right -= 1
            else:
                left += 1

        return max

```
