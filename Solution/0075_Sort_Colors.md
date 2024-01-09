# Sort Colors / 颜色分类

Leetcode: https://leetcode.com/problems/sort-colors/

中文力扣：https://leetcode.cn/problems/sort-colors/

## Description / 题目描述

Given an array `nums` with `n` objects colored red, white, or blue, sort them [in-place](https://en.wikipedia.org/wiki/In-place_algorithm) so that objects of the same color are adjacent, with the colors in the order red, white, and blue.

We will use the integers `0`, `1`, and `2` to represent the color red, white, and blue, respectively.

You must solve this problem without using the library's sort function.

给定一个包含红色、白色和蓝色、共 `n` 个元素的数组 `nums` ，[原地](https://baike.baidu.com/item/%E5%8E%9F%E5%9C%B0%E7%AE%97%E6%B3%95)对它们进行排序，使得相同颜色的元素相邻，并按照红色、白色、蓝色顺序排列。

我们使用整数 `0`、 `1` 和 `2` 分别表示红色、白色和蓝色。

必须在不使用库内置的 sort 函数的情况下解决这个问题。

## Solution 1: Bucket Sort / 桶排序

Iterate through the given array `nums`, using a variable `bucket` to track the frequency of 0, 1, and 2.

After the iteration, we disregard the original distribution of the given array `nums` and simply reconstruct `nums` (in place) based on the elements in `bucket`.

The time complexity of this algorithm is `O(n)`.

遍历给定数组 `nums`，使用一个变量 `bucket`记录0，1，2出现的次数。

遍历完成后，我们忽略给定数组 `nums`原本的分布，只需要根据 `bucket`中的元素(原地)重构 `nums`即可。

本算法时间复杂度为 `O(n)`

Java:

```java
class Solution {
    public void sortColors(int[] nums) {
        int[] bucket = {0,0,0};
        for (int num : nums){
            bucket[num] ++;
        }

        int curNum = 0;
        int cumulativeIndex = 0;

        for (int value : bucket){
            for (int i = 0; i < value; i++){
                nums[cumulativeIndex] = curNum;
                cumulativeIndex ++;
            }
            curNum ++;
        }
    }
}

```

Python:

```python
class Solution:
    def sortColors(self, nums: List[int]) -> None:
        bucket = [0,0,0]
        for num in nums:
            bucket[num] += 1

	curNum = 0
        cumulativeIndex = 0

        for num in bucket:
            for _ in range(num):
                nums[cumulativeIndex] = curNum
                cumulativeIndex += 1
            curNum += 1

```

## Solution 2: Two Pointers / 双指针

We can also solve this problem using the two-pointer technique, setting two variables: `left` and `right` to track the left and right boundaries, respectively. Then, we iterate through the given array `nums`. During the iteration, we move all the 0s to the left side of `nums` and all the 2s to the right side (then all the 1s will definitely be in the middle).

During the iteration, there are three possible cases, and actions are as follows:

1. If the current number is 0, we swap the current 0 with the number at the left boundary, then move the left boundary to the right.
2. If the current number is 2, we swap the current 2 with the number at the right boundary, then move the right boundary to the left.
3. If the current number is 1, we ignore it and make no changes to any boundary.

If the current index being searched reach the right boundary, end the iteration.

This method only focuses on the current number's value and the boundary updates, without concerning the number swapped to the current position from the boundary.

The time complexity of this solution is `O(n)`.

我们亦可以用双指针来解本题，设定两个变量：`left`和 `right`，分别记录左边界和右边界，之后遍历给定数组 `nums`，在遍历途中，将所有的0移动到 `nums`的左边，将所有的2移动到 `nums`的右边(此时所有的1一定在0和2的中间)

遍历途中会有三钟可能的情况，具体做法为：

1. 如果当前数字等于0，我们将当前的0和左边界上的数字交换，之后向右移动左边界
2. 如果当前数字等于2，我们将当前的2和右边界上的数字交换，之后向左移动右边界
3. 如果当前数字等于1，忽略，不对任何边界做改变

若当前搜索的下标与右边界重合，退出遍历。

此方法只关心当前数字的值和边界更新，而并不关注边界上交换到当前位置的数字的值

本解法时间复杂度为 `O(n)`

Java:

```java
class Solution {
    public void sortColors(int[] nums) {
        int left = 0;
        int right = nums.length - 1;
        int curr = 0;

        while(curr <= right){
            if (nums[curr] == 0){ // Make sure every element get checked
                swap(nums, curr, left);
                curr ++;
                left ++;
            }else if (nums[curr] == 2){
                swap(nums, curr, right);
		// Update right only because we don't know the value of the number got swapped from right to curr
                right --;
            }else {
                curr ++;
            }
        }
}

    public void swap(int[] nums, int p1, int p2){
        int temp = nums[p1];
        nums[p1] = nums[p2];
        nums[p2] = temp;
    }
}

```

Python:

```python
class Solution:
    def sortColors(self, nums: List[int]) -> None:
        left = 0
        right = len(nums) - 1
        curr = 0

        def swap(nums: List[int], p1: int, p2: int):
            temp = nums[p1]
            nums[p1] = nums[p2]
            nums[p2] = temp

        while(curr <= right): # Make sure every element got checked
            if nums[curr] == 0:
                swap(nums, curr, left)
                curr += 1
                left += 1
            elif nums[curr] == 2:
                swap(nums, curr, right)
		# Update right only because we don't know the value of the number got swapped from right to curr
                right -= 1
            else:
                curr += 1

```
