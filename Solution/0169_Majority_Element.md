# [169. Majority Element](https://leetcode.com/problems/majority-element/)

[中文版本](/Solution_CN/0169_Majority_Element_CN.md)

## Solution 1: Counting

This Solution is relatively stright forward, we can get the answer by count the appearance of each number, by using Hashmap

This solution has a `O(n)` Time complexity and `O(n)` Space complexity.

Java:

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

// Tong
```

Python:

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

# Tong
```

## Solution 2: Math

According to the question, majority element must exists in the given array, if we sort the given array, we must have the answer at index[nums.length / 2]

This solution has a `O(n log n) `time complexity due to sorting, but it only has a `O(1) `space complexity.

Java:

```java
class Solution {
    public int majorityElement(int[] nums) {
        Arrays.sort(nums);
        return nums[nums.length / 2];
    }
}

// Tong
```

Python:

```python
class Solution:
    def majorityElement(self, nums: List[int]) -> int:
        nums.sort()
        return nums[int(len(nums) / 2)]


# Tong
```
