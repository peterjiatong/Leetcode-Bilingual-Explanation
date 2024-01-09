# Contains Duplicate / 存在重复元素

Leetcode: https://leetcode.com/problems/contains-duplicate/

中文力扣：https://leetcode.cn/problems/contains-duplicate/

## Description / 题目描述

Given an integer array `nums`, return `true` if any value appears **at least twice** in the array, and return `false` if every element is distinct.

给你一个整数数组 `nums` 。如果任一值在数组中出现 **至少两次** ，返回 `true` ；如果数组中每个元素互不相同，返回 `false` 。

## Solution: HashSet / 哈希集

Use a hash table to store the numbers that have seen. Then, iterate through the given array `nums`. If the current number has not appeared before (it does not exist in the hash set), store it in the hash set. If it has appeared before (it exists in the hash set), then return `true`.

Since accessing an element in the hash set has a time cost of `O(1)`, the time complexity of this solution is `O(n)`.

创建一个哈希表用于储存出现过的数字，之后遍历给定数组 `nums`，若当前数字之前没出现过(当前数字不存在于哈希集中)，则存入哈希集中，若出现过(当前数字存在于哈希集中)，则返回 `true`

因为访问哈希集中的元素的时间代价为 `O(1)`，所以本解法时间复杂度为 `O(n)`

Java:

```java
class Solution {
    public boolean containsDuplicate(int[] nums) {
        HashSet<Integer> seen = new HashSet<>();
        for (int num: nums){
            if (seen.contains(num)){
                return true;
            }
            seen.add(num);
        }

        return false;
    }
}

```

Python:

```python
class Solution:
    def containsDuplicate(self, nums: List[int]) -> bool:
        seen = set()
        for num in nums:
            if num in seen:
                return True
            seen.add(num)
        return False

```
