# Contiguous Array / 连续数组

Leetcode: https://leetcode.com/problems/contiguous-array/

中文力扣：https://leetcode.cn/problems/contiguous-array/

## Description / 题目描述

Given a binary array `nums`, return *the maximum length of a contiguous subarray with an equal number of `0` and*  `1`.

给定一个二进制数组 `nums` , 找到含有相同数量的 `0` 和 `1` 的最长连续子数组，并返回该子数组的长度。

## Solution: Hashmap / 哈希表

We can approach this problem as a prefix sum problem. If we consider the 0s in the array as -1s, we can transform this problem into finding the *longest contiguous subarray with a sum of 0.*

If the prefix sum at the current position `nums[i]` is -1, we just need to find the index `nums[j]` of the previous prefix sum that was -1. This allows us to find the subarray with a sum of 0 as `nums[j+1:i]`. 

(For example, we have a prefix sum for index `i = 9` is -1, which means the sum of `nums[0 : 9]` is -1, if we have another index `j = 6` with a prefix sum of -1, then `nums[7 : 9]` would gurantee to have a sum of 0. )

With this idea in mind, we create a hash table called `seen` to store [unseen prefix sum, its index].

Whenever we encounter a previously seen prefix sum, we can determine the length by subtracting the index stored in `seen` for that prefix sum from the current index `i`. Since `seen` only records unseen prefix sums, we can be sure that this length is optimal.

The time complexity of this algorithm is `O(n)`.

我们可以将此问题看为一个前缀和问题，若将数组中的0视为-1，我们就可以把这道题转化为找到*和为0的最长的连续子数组。*

若当前 `nums[i]`的前缀和为-1，那我们只需要找到上一个前缀和为-1的下标 `nums[j]`，就可以找到和为0的子数组 `nums[j+1, i]`

（例如，下标 `i = 9`的前缀和为-1，意味着 `nums[0 : 9]`的和为-1，如果我们有另一个下标 `j = 6`的前缀和也为-1，那么 `nums[7 : 9]`的和一定为0。）

基于此想法，我们创建一个哈希表 `seen`，用于存放[未出现过的前缀和，其下标]

每当我们找到了一个出现过的前缀和，我们就可以找此处的下标和 `seen`中记录此前缀和的下标+1的长度，由于 `seen`只记录未出现过的前缀和，我们可以确定此处的下标和 `seen`中记录此前缀和的下标+1的长度一定是最优的。

此算法时间复杂度为 `O(n)`

Java

```java
class Solution {
    public int findMaxLength(int[] nums) {
        Map<Integer, Integer> seen = new HashMap<>();
        int max = 0;
        int presum = 0;
        seen.put(0, -1); // Initialize seen as (0,-1), indicate that before iterate nums, presum = 0

        for (int i = 0; i < nums.length; i++){
            if (nums[i] == 1) presum++;
            else presum--;

            if (seen.containsKey(presum)){
                if (i - seen.get(presum) > max) max = i - seen.get(presum);
            } else {
                seen.put(presum, i);
            }
        }

        return max;
    }
}

```

 Python

```Python
class Solution:
    def findMaxLength(self, nums: List[int]) -> int:
        seen = dict()
        max = 0
        presum = 0
        seen[0] = -1 # Initialize seen as (0,-1), indicate that before iterate nums, presum = 0

        for i in range(len(nums)):
            if nums[i] == 1:
                presum += 1
            else:
                presum -= 1

            if presum in seen:
                if (i - seen[presum] > max):
                    max = i - seen[presum]
            else:
                seen[presum] = i
  
        return max

```
