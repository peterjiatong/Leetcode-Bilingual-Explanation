# Two Sum / 两数之和

Leetcode: https://leetcode.com/problems/two-sum/

中文力扣: https://leetcode.cn/problems/two-sum/


## Description / 题目描述

Given an array of integers `nums` and an integer `target`, return  *indices of the two numbers such that they add up to `target`* .

You may assume that each input would have  ***exactly* one solution** , and you may not use the *same* element twice.

You can return the answer in any order.

给定一个整数数组 `nums` 和一个整数目标值 `target`，请你在该数组中找出 ***和为目标值*** *`target`*  的那 **两个** 整数，并返回它们的数组下标。

你可以假设每种输入只会对应一个答案。但是，数组中同一个元素在答案里不能重复出现。

你可以按任意顺序返回答案。


## Solution 1: Brute-force / 蛮力法

The simplest solution is to use nested for loops. The outer loop iterates through all elements, while the inner loop iterates from the next index of the current element in the outer loop to the last element, checking if the sum of any two elements equals `target`

This approach has a O(n^2) time Complexity

最简单的解法是使用for循环的嵌套，外层循环遍历所有元素，而内层循环从外层当前元素的下一个元素遍历到最后一个元素，依次检查两个元素之和是否等于 `target`

此解法时间复杂度为 `O(n^2)`



Java

```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        for (int i = 0; i < nums.length - 1; i++) {
            for (int j = i + 1; j < nums.length; j++) {
                if (nums[i] + nums[j] == target) {
                    return new int[]{i, j};
                }
            }
        }
        // In case no solution found
        return new int[]{};
    }
}

```

Python:

```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        for i in range(len(nums) - 1):
            for j in range(i + 1, len(nums)):
                if nums[i] + nums[j] == target:
                    return [i, j]
        return [] # In case no solution found
```


## **Solution 2: Hash-Map / 哈希表**

Utilizing a hash-map for solving the problem is a more sophisticated approach, as accessing a hash-map has a time complexity of `O(1)`, significantly reducing the execution time of the code.

We use a hash-map to store pairs of `(target - num[i], i)`, where `i` is the index of the elements in the array.

When iterating through the array `nums`, if we find that `target - num[i]` is already in the hash-map, we have found our solution (i.e. the current index `i` and the value of `target - num[i]` in the hash table). Otherwise, we put `(target - num[i], i)` in the hash-map.

This approach has a time complexity of `O(n)`.

使用哈希表解题是更加精妙的方法，因为访问哈希表是时间消耗为 `O(1)`，可以显著减少代码运行时间

我们使用一个哈希表用于存放（`target` - `num[i]`, `i`), `i` 为元素的下标

对数组nums进行一次遍历，若发现 `target` - `num[i]` 已在哈希表中，则我们找到了答案 (即当前坐标i 和 哈希表中 `target `- `num[i]`的值)，反之，则将(`target` - `num[i]`,` i`) 存入哈希表中

此解法时间复杂度为O(n)


Java:

```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        HashMap<Integer,Integer> values = new HashMap<>();
        for (int i = 0; i < nums.length; i++){
            if(values.containsKey(nums[i])){ // If we found nums[i] in the hashmap, return
                return new int[] {i, values.get(nums[i])};
            }
            values.put(target - nums[i], i);
        }
    // In case no solution found
    return new int[]{};
    }
}

```

Python:

```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        # dict() in python is based on hashmap
        values = dict()
        for i in range(0, len(nums)):
            # If we found nums[i] in the hashmap, return
            if nums[i] in values:
                return (i, values[nums[i]])
            values[target - nums[i]] = i
```
