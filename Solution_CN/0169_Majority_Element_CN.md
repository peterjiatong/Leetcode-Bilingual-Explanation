# [169. 多数元素](https://leetcode.com/problems/majority-element/)

[English Ver.](/Solution/0169_Majority_Element.md)

## 解法1：计数法

这个解法思路相对直截了当。我们可以通过使用哈希表来计算每个数字出现的次数，从而得到答案。

该解决方案的时间复杂度为 `O(n)`，空间复杂度也为 `O(n)`。

Java

```java
class Solution {
    public int majorityElement(int[] nums) {
	// Use a map to count appearance of numbers
        Map<Integer, Integer> map = new HashMap<>();
        for (int i = 0; i < nums.length; i++){
            if(!map.containsKey(nums[i])){
                map.put(nums[i], 1);
            }else {
                map.put(nums[i], map.get(nums[i]) + 1);
            }

            if (map.get(nums[i]) > nums.length / 2){ // If num[i] has a value greater than len(nums) / 2, return
                return nums[i];
            }
        }

	// A return is required for java
        return 0;
    }
}

// Tong, 9/20/2023
```

Python

```python
class Solution:
    def majorityElement(self, nums: List[int]) -> int:
      	# We use a dict because dict functions the same as a hashmap in python
	map = {}
        for num in nums:
            if not num in map:
                map[num] = 1
            else:
                map[num] += 1
  
            if map[num] > (len(nums) / 2): # If current num has a value greater than len(nums) / 2, return
                    return num

        return 0

# Tong, 9/20/2023
```

## 解法2：数学法

根据题目可知，多数元素必定存在于给定的数组中。如果我们对给定数组进行排序，答案一定会出现在索引 `nums.length / 2` 处。

由于排序的原因，这个解决方案的时间复杂度为` O(nlogn)`，但其空间复杂度仅为` O(1)`。

Java

```java
class Solution {
    public int majorityElement(int[] nums) {
        Arrays.sort(nums);
        return nums[nums.length / 2];
    }
}

// Tong, 9/20/2023
```

Python

```python
class Solution:
    def majorityElement(self, nums: List[int]) -> int:
        nums.sort()
        return nums[int(len(nums) / 2)]


# Tong, 9/20/2023
```
