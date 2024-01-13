# Move Zeroes / 移动零

Leetcode: https://leetcode.com/problems/move-zeroes/

中文力扣: https://leetcode.cn/problems/move-zeroes/

## Description / 题目描述

Given an integer array `nums`, move all `0`'s to the end of it while maintaining the relative order of the non-zero elements.

**Note** that you must do this in-place without making a copy of the array.

给定一个数组 `nums`，编写一个函数将所有 `0` 移动到数组的末尾，同时保持非零元素的相对顺序。

**请注意** ，必须在不复制数组的情况下原地对数组进行操作。

## Solution 1: Pointer / 指针

We first create a pointer `count` to count the number of non-zero elements in the array. As we are iterating through the array, if we find a element that is non-zero, put it in the front of the array by using the count pointer. As we find more non-zero elements, simply put them into the "`count + 1`" th index. After iterating through `nums`, `count` will have the number of non-zero elements. We. can then add `n - count` number of 0's to the end of the array.

Time complexity of this method is `O(n)`. However this method will write in 

我们首先创建一个指针 `count` 来计算数组中非零元素的数量。在遍历数组时，如果我们找到一个非零元素，就使用 `count` 指针将其放到数组的前面。当我们找到更多非零元素时，简单地将它们放入 "`count + 1`" 个索引的位置。在遍历完 `nums` 之后，`count` 将会有非零元素的数量。然后，我们可以在数组的末尾添加 `n - count` 个 0。

这种方法的时间复杂度为 `O(n)`。然而这种方法将会在数组中进行 `n` 次写入操作。

Java:

```Java
class Solution {
    public void moveZeroes(int[] nums) {
  
    }
}
```

Python:

```python
class Solution:
    def moveZeroes(self, nums: List[int]) -> None:
        """
        Do not return anything, modify nums in-place instead.
        """
        count = 0
        for i in nums:
            if i != 0:
                nums[count] = i
                count += 1
  
        while count < len(nums):
            nums[count] = 0
            count += 1
```

## Solution 2: Two Pointers / 双指针
