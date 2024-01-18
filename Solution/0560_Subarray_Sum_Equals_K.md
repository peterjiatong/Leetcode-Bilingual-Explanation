# Subarray Sum Equals K / 和为 K 的子数组

Leetcode: https://leetcode.com/problems/subarray-sum-equals-k/

中文力扣：https://leetcode.cn/problems/subarray-sum-equals-k/

## Description / 题目描述

Given an array of integers `nums` and an integer `k`, return *the total number of subarrays whose sum equals to* `k`.

A subarray is a contiguous **non-empty** sequence of elements within an array.

给你一个整数数组 `nums` 和一个整数 `k` ，请你统计并返回  *该数组中和为 `k` 的子数组的个数 * 。

子数组是数组中元素的连续非空序列。

## Solution 1: Prefix Sum / 前缀和

To calculate the sum of subarrays in a given array `nums`, an array `presum` with a length of one more than `nums` is used to store all prefix sums. Initialize `presum[0]` to 0, then iterate through the array `nums`, updating `presum[i + 1] = presum[i] + nums[i]`.

With this setup, the sum of the subarray `nums[i : j]` should be `presum[j] - presum[i]`. By using a nested for loop, we can record the number of occurrences where the difference between any two prefix sums equals `k`.

This algorithm has a time complexity of O(n^2), use python will exceeds the time limit constraints of LeetCode, and therefore is not recommended.

使用一个比给定数组 `nums`的长度多1的数组 `presum`存储所以的前缀和，将 `presum[0]`初始化为0，之后遍历数组 `nums`，更新数组 `presum[i + 1] = presum[i] + nums[i]`

此时，子数组 `nums[i : j]`的和就应该是 `presum[j] - presum[i]`，我们只需使用嵌套的for循环，记录所有子数组的前缀和的差等于 `k`出现的次数。

此算法时间复杂度为O(n^2)，使用python会超过leetcode的时间限制要求，故不推荐

Java

```java
class Solution {
    public int subarraySum(int[] nums, int k) {
        int[] presum = new int[nums.length + 1];
        int count = 0;

        for (int i = 0; i < nums.length; i++){
            presum[i + 1] = presum[i] + nums[i];
        }

        for (int i = 0; i < presum.length - 1; i++){
            for (int j = i + 1; j < presum.length; j++){
                if (presum[j] - presum[i] == k) count++;
            }
        }

        return count;
    }
}

```

Python

```python
class Solution:
    def subarraySum(self, nums: List[int], k: int) -> int:
        presum = [0] * (len(nums) + 1)
        count = 0

        for i in range(len(nums)):
            presum[i + 1] = presum[i] + nums[i]
  
        for i in range(len(presum) - 1):
            for j in range(i + 1, len(presum)):
                if presum[j] - presum[i]  == k:
                    count += 1
  
        return count
  # Exceeds time limit
```

## Solution 2: Hashmap / 哈希表

Solution 2 follows a similar concept as Solution 1, but it uses a different data structure, utilizes a hash table.

Frirstly, create a hash table `presum` to store the prefix sums and their frequencies; an integer `count` to keep track of the number of subarrays that meet the condition; and an integer `sum` to record the current prefix sum at index i.

As you iterate through the array, if `presum` contains `sum - k`, then update `count += presum.get(sum - k)`. After that, add `sum` to `presum`. If `sum` already exists in `presum`, increment its value by 1.

(For example, with the array [1, 2, 3, -4, 2, 2], the prefix sums would be [1, 3, 6, 2, 6, 8]. If k = 2, when the index is at 5, sum = 8, and we should look for the frequency of sum - k, which is 4, in the array.)

The time complexity of this algorithm is `O(n)`.

解法2和解法1的思路基本一致，只是使用的数据结构有所区别，本解法将使用哈希表

首先创建一个用于储存前缀和及其出现次数的哈希表 `presum`；和一个整数count，用于记录满足条件的子数组的数量；以及一个整数`sum`，用于记录当前下标i的前缀和。

遍历数组时，若presum中含有sum - k, 更新 `count += presum.get(sum - k)`。之后将 `sum `添加至 `presum`中，若 `presum`中已经存在 `sum`，就将其的值 `+1`

(例如，数组[1, 2 , 3, -4, 2, 2]，其前缀和应为[1, 3, 6, 2, 6, 8], 若k = 2, 当下标处于5时，sum = 8，我们就应该在数组中寻找sum - k，也就是6出现的次数)

此算法的时间复杂度为`O(n)`

Java

```Java
class Solution {
    public int subarraySum(int[] nums, int k) {
        HashMap<Integer, Integer> presum = new HashMap<>();
        int sum = 0;
        int count = 0;
        presum.put(0, 1);

        for (int i = 0; i < nums.length; i++){
            sum += nums[i];
            if (presum.containsKey(sum - k)){
                count += presum.get(sum - k);
            }
            presum.put(sum, presum.getOrDefault(sum, 0) + 1);
        }

        return count;
    }
}

```

Python

```python
class Solution:
    def subarraySum(self, nums: List[int], k: int) -> int:
        presum = {}
        count = 0
        sum = 0
        presum[0] = 1

        for i in range(len(nums)):
            sum += nums[i]
            if sum - k in presum:
                count += presum[sum - k]
            presum[sum] = presum.get(sum, 0) + 1
  
        return count

```
