# [217. Contains Duplicate](https://leetcode.com/problems/contains-duplicate/)

[中文版本](/Solution_CN/0217_Contains_Duplicate_CN.md)

## Solution: HashSet

A HashSet is one of the best data structures for these types of questions since it only requires `O(1) `time complexity for both search and insertion. We can simply traverse the given array, `nums.` If `nums[i]` is in the HashSet, return `true`; otherwise, add `nums[i]` to the HashSet.

This Solution has an `O(n)` time complexity and an `O(n)` space complexity(one HashSet used)

Java:

```java
class Solution {
    public boolean containsDuplicate(int[] nums) {
	// Use HashSet because it take O(1) for both search and insert
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

// Tong
```

Python:

```python
class Solution:
    def containsDuplicate(self, nums: List[int]) -> bool:
        # set in python functions the same as hashset
        seen = set()
        for num in nums:
            if num in seen:
                return True
            seen.add(num)
        return False

# Tong
```
