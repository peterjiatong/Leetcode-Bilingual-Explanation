# [Two Sum](https://leetcode.com/problems/two-sum/)

[中文版本](/Users/to/Solution_CN/0001_Two_Sum_CN.md)

## Solution

**Solution 1: Brute-force**

The simplest solution is to go through every two pair and check if they can sum up to the target, by using 2 for-loop, where the outer loop iterates from the first element to the second last element(notes as i), and the inner loop iterates from i to the last element.

This approach has a O(n^2) time Complexity

### Java

```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        // Iterates from index 0 to nums.length - 1
        for (int i = 0; i < nums.length - 1; i++) {
            // Iterates from i to nums.length
            for (int j = i + 1; j < nums.length; j++) {
                // If their sum equals to target, return {i, j}
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

### Python

```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        # Iterates from index 0 to nums.length - 1
        for i in range(len(nums) - 1):
            # Iterates from i to nums.length
            for j in range(i + 1, len(nums)):
                # If their sum equals to target, return {i, j}
                if nums[i] + nums[j] == target:
                    return [i, j]
```

**Solution 2: Hash-Map**
For this solution, we will store (target - num[i], index i) into a hashmap. while we traverse the given array nums, if we found nums[i] in the hashmap, we found the answer.

This is an efficient approach because hashmap can search it's key in O(1) time, so the time complexity for this solution is O(n).

### Java

```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        // Creates a hash map the takes an integer as key and an integer as value
        HashMap<Integer,Integer> values = new HashMap<>();
        // Iterates the given array nums
        for (int i = 0; i < nums.length; i++){
            // If we found nums[i] in the hashmap, return
            if(values.containsKey(nums[i])){
                return new int[] {i, values.get(nums[i])};
            }
            // Else, put target - nums[i] and its index in the hashmap
            values.put(target - nums[i], i);
        }
    // In case no solution found
    return new int[]{};
    }
}
```

### Python

```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        # because dict() in python in based on hashmap, we don't have to pecifically set up a hashmap
        values = dict()
        # Iterates the given array nums
        for i in range(0, len(nums)):
            # If we found nums[i] in the hashmap, return
            if nums[i] in values:
                return (i, values[nums[i]])
            # Else, put target - nums[i] and its index in the hashmap
            values[target - nums[i]] = i
```
