# Majority Element / 多数元素

Leetcode: https://leetcode.com/problems/majority-element/

中文力扣：https://leetcode.cn/problems/majority-element/

## Description / 题目描述

Given an array `nums` of size `n`, return  *the majority element* .

The majority element is the element that appears more than `⌊n / 2⌋` times. You may assume that the majority element always exists in the array.

给定一个大小为 `n` 的数组 `nums` ，返回其中的多数元素。多数元素是指在数组中出现次数 **大于** `⌊ n/2 ⌋` 的元素。

你可以假设数组是非空的，并且给定的数组总是存在多数元素。

## Solution 1: Counting / 计数法

The first solution is relatively simple and straightforward. We record each number and its frequency in a hash table. Then, we iterate through the hash table, any number that appears more than `n/2` times is the answer to this problem.

The time complexity of this method is `O(n)`.

第一种解法相对简单直接，我们将每种数字和其出现的次数记录在一个哈希表中，之后遍历哈希表，任意数字出现的次数大于 `n/2`就是本题的答案

此方法时间复杂度为 `O(n)`

Java:

```java
class Solution {
    public int majorityElement(int[] nums) {
        Map<Integer, Integer> map = new HashMap<>();
	int half = nums.length / 2;

        for (int i = 0; i < nums.length; i++){
            if(!map.containsKey(nums[i])){
                map.put(nums[i], 1);
            }else {
                map.put(nums[i], map.get(nums[i]) + 1);
            }

            if (map.get(nums[i]) > half){
                return nums[i];
            }
        }

        return 0; // A return is required for java
    }
}

```

Python:

```python
class Solution:
    def majorityElement(self, nums: List[int]) -> int:
	map = {}
	half = len(nums) / 2
        for num in nums:
            if not num in map:
                map[num] = 1
            else:
                map[num] += 1
  
            if map[num] > half:
                    return num

        return 0

```

## Solution 2: Math / 数学法

According to the description, we know that there is only one solution to this problem, and because it appears more times than half the length of the given array, if we sort the given array `nums`, the number that appears at `nums[nums.length / 2]` is definitely the answer.

Since a sorting algorithm is used, the time complexity of this method is `O(n log n)`.

根据题目描述，已知本题有且只有一个解，又因其出现次数超过给定数组长度的一般，当我们对给定数组 `nums`排序后，出现在 `nums[nums.length / 2]`的数字一定就是答案

因使用了排序算法，此方法的时间复杂度为 `O(n log n)`

Java:

```java
class Solution {
    public int majorityElement(int[] nums) {
        Arrays.sort(nums);
        return nums[nums.length / 2];
    }
}

```

Python:

```python
class Solution:
    def majorityElement(self, nums: List[int]) -> int:
        nums.sort()
        return nums[int(len(nums) / 2)]

```
