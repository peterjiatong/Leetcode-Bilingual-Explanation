# Two Sum / 两数之和

Leetcode: https://leetcode.com/problems/two-sum/

中文力扣: https://leetcode.cn/problems/two-sum/

## Description / 题目描述

Given an array of integers `nums` and an integer `target`, return _indices of the two numbers such that they add up to `target`_ .

You may assume that each input would have **_exactly_ one solution** , and you may not use the _same_ element twice.

You can return the answer in any order.

给定一个整数数组 `nums` 和一个整数目标值 `target`，请你在该数组中找出 **_和为目标值_** _`target`_ 的那 **两个** 整数，并返回它们的数组下标。

你可以假设每种输入只会对应一个答案。但是，数组中同一个元素在答案里不能重复出现。

你可以按任意顺序返回答案。

## Constraints **/ 提示**

- `2 <= nums.length <= 10^4`
- `-10^9 <= nums[i] <= 10^9`
- `-10^9 <= target <= 10^9`
- **Only one valid answer exists. / 只会存在一个有效答案**

## Solution 1: Brute-force / 蛮力法

The brute force solution uses a nested loop to loop over each element `x` in the given array `nums`, and to check if there is another element `y` exists such that `x + y = target`

This approach has a time complexity of `O(n^2)`

蛮力法使用 for 循环的嵌套来遍历给定数组 `nums` 中的每个元素 `x`，并检查是否存在另一个元素 `y` 使得 `x + y = target`

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

Python

```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        for i in range(len(nums) - 1):
            for j in range(i + 1, len(nums)):
                if nums[i] + nums[j] == target:
                    return [i, j]
        return [] # In case no solution found
```

## **Solution 2: Hash Map / 哈希表**

Using a hash table can significantly reduce the runtime because accessing elements in a hash map has a time cost of `O(1)`.

Using a hash map to store the difference between `target` and the current element `nums[i]`, along with the index of the current element, or (`target` - `nums[i]`, `i`).

Then we traverse the array `nums` and check if the current element is already in the hash table. If it exists, it means we have found the answer (i.e., the index of the current element `i` and the value of the current element in the hash table). Otherwise, we store (`target` - `nums[i]`, `i`) in the hash table.

The time complexity of this solution is `O(n)`.

使用哈希表可以显著减少代码运行时间，因为在哈希表中访问元素的时间成本为 `O(1)`

创建一个哈希表用于存放 `target`与当前元素 `nums[i]`的差和当前元素的下标，即（`target` - `num[i]`, `i`)

之后对数组 `nums`进行遍历，检查当前元素是否已在哈希表中，如果存在，表明我们找到了答案 (即当前元素的下标 `i`和哈希表中存在的当前元素的值)，反之，则将(`target` - `num[i]`,` i`) 存入哈希表中

此解法时间复杂度为 O(n)

Java

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

Python

```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        # dict() in python is based on hash map
        values = dict()
        for i in range(0, len(nums)):
            # If we found nums[i] in the hash map, return
            if nums[i] in values:
                return (i, values[nums[i]])
            values[target - nums[i]] = i
```
