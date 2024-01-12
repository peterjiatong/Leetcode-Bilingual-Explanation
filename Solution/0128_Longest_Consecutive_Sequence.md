# Longest Consecutive Sequence /  最长连续序列

Leetcode: https://leetcode.com/problems/longest-consecutive-sequence/

中文力扣：https://leetcode.cn/problems/longest-consecutive-sequence/description/

## Description / 题目描述

Given an unsorted array of integers `nums`, return *the length of the longest consecutive elements sequence.*

You must write an algorithm that runs in `O(n)` time.

给定一个未排序的整数数组 `nums` ，找出数字连续的最长序列（不要求序列元素在原数组中连续）的长度。

请你设计并实现时间复杂度为 `O(n)` 的算法解决此问题。

## Solution: HashSet / 哈希集

This problem requires a solution in O(n) time, so we cannot use sorting algorithms*

The definition of a consecutive sequence in the problem is a sequence with an arithmetic difference of 1. We can solve this problem using a HashSet:

First, store all the numbers in a HashSet. Then, iterate through the HashSet:

1. If the current number - 1 exists in the HashSet, it means this number is possibly part of the longest consecutive sequence but not the first element.
2. If the current number - 1 does not exist in the HashSet, it means this number could be the first element of the possible longest consecutive sequence. We check if the number + 1 exists in the HashSet, and if it does, we use an int variable to track the length of this sequence and update the current number.

After the iteration, return the length of the longest sequence found. Since we are using a HashSet (with O(1) time complexity for element access), the time complexity of this algorithm is O(n).

此题要求在 `O(n)`时间内解决，所以我们不能使用排序算法*

题目中对连续序列的定义为差为1的等差数列，我们首先将所有数字存入一个集合中，之后遍历该合集：

1. 若当前数字 - 1存在于集合中，表明该数字是可能的最长的连续序列中的元素，但一定不是第一个元素。
2. 若当前数字 - 1不存在于集合中，表明该数字有可能是最长的连续序列的第一个元素，我们检查该数字+1的数字是否存在于集合中，若存在，使用一个整数变量记录此数列的长度，并更新当前数字

遍历结束后，返回最长的序列的长度，因为使用了哈希集(其访问元素时间为`O(1)`)，此算法的时间复杂度为`O(n)`

(*Some solutions that use sorting algorithms may pass the LeetCode tests but are not discussed here because they do not meet the requirement of O(n) time complexity. 部分使用排序算法的解法可以通过力扣的检测，但因为时间复杂度不合格，不在这里进行赘述)

Java

```java
class Solution {
    public int longestConsecutive(int[] nums) {
        Set<Integer> seen = new HashSet<>();
        int longest = 0;
        int curr = 0;
        int currLength = 0;
        for (int num : nums){
            seen.add(num);
        }

        for (int num: seen){
            if (!seen.contains(num - 1)){
                curr = num;
                currLength = 0;

                while(seen.contains(curr)){
                    curr++;
                    currLength++;
                }

                if (currLength > longest) longest = currLength;
            }
        }

        return longest;
    }
}

```

Python

```python
class Solution:
    def longestConsecutive(self, nums: List[int]) -> int:
        seen = set(nums)
        longest = 0

        for num in seen:
            if num - 1 not in seen:
                curr = num
                currLength = 0

                while(curr in seen):
                    curr += 1
                    currLength += 1

                if currLength > longest:
                    longest = currLength
  
        return longest

```
