# Move Zeroes / 移动零

Leetcode: https://leetcode.com/problems/move-zeroes/

中文力扣: https://leetcode.cn/problems/move-zeroes/

## Description / 题目描述

Given an integer array `nums`, move all `0`'s to the end of it while maintaining the relative order of the non-zero elements.

**Note** that you must do this in-place without making a copy of the array.

给定一个数组 `nums`，编写一个函数将所有 `0` 移动到数组的末尾，同时保持非零元素的相对顺序。

**请注意** ，必须在不复制数组的情况下原地对数组进行操作。

## Solution: Pointer / 指针

First, we create a pointer `pivot` to count the number of non-zero elements in the array. While traversing the array, if we find a non-zero number, we update `nums[pivot]` to that number, then update `pivot += 1`. After traversing `nums`, update all numbers in `nums[pivot : -1]` to 0.

The time complexity of this method is `O(n)`.

我们首先创建一个指针 `pivot` 来计算数组中非零元素的数量。在遍历数组时，如果我们找到一个非零数，就更新`nums[pivot]`为该数，然后更新`pivot += 1`。在遍历完 `nums` 之后，将`nums[pivot : -1]`中的所有数字更新为0即可

这种方法的时间复杂度为 `O(n)`。

Java:

```Java
class Solution {
    public void moveZeroes(int[] nums) {
        if (nums.length == 1) return;

        int pivot = 0;
        for (int i = 0; i < nums.length; i++){
            if (nums[i] != 0){
                nums[pivot] = nums[i];
                pivot++;
            }
        }

        for (int i = pivot; i < nums.length; i++){
            nums[i] = 0;
        }
    }
}

```

Python:

```python
class Solution:
    def moveZeroes(self, nums: List[int]) -> None:
        pivot = 0
        for i in nums:
            if i != 0:
                nums[pivot] = i
                pivot += 1
  
        while pivot < len(nums):
            nums[pivot] = 0
            count += 1

```
