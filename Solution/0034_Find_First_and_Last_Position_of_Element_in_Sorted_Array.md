# [34. Find First and Last Position of Element in Sorted Array](https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/)

[中文版本]()

## Solution: Binary Search

Instead of finding the answer in a single pass, this solution divides the problem into two parts:

1. Find the first occurrence of the element in a sorted array.
2. Find the last occurrence of the element in the same array.

Each part involves a straightforward binary search. Since binary search has a time complexity of O(log n), the overall complexity of this approach remains O(log n) as well.

```java
class Solution {
    public int[] searchRange(int[] nums, int target) {
	// Corner-case
        if (nums == null || nums.length == 0) return new int[] {-1, -1};

      	// Find the first occurrence
	int left = firstPosition(nums, target);
        if(left == -1) return new int[]{-1, -1}; // if we didn't find any element equals to the target, return {-1, -1}
	// Find the last occurrence
        int right = lastPosition(nums, target);

        return new int[]{left, right};
    }

    public int firstPosition(int[] nums, int target){
        int left = 0;
        int right = nums.length - 1;
        int mid = 0;

        while(left + 1 < right){
            mid = left + (right - left) / 2;
            if (nums[mid] < target) left = mid;
            else right = mid; // If nums[mid] == target, we set right = mid instead of return, because we need to find the first occurrence.
        }

	// Post processing
        if(nums[left] == target) return left;
        if(nums[right] == target) return right;
  
        return -1;
    }

    public int lastPosition(int[] nums, int target){
        int left = 0;
        int right = nums.length - 1;
        int mid = 0;

        while(left + 1 < right){
            mid = left + (right - left) / 2;
            if (nums[mid] > target) right = mid;
            else left = mid; // If nums[mid] == target, we set left = mid instead of return, because we need to find the last occurrence.
        }

	// Post processing
        if(nums[right] == target) return right; // check nums[right] first to avoid edge case
        if(nums[left] == target) return left;
  
        return -1;
    }
}

// Tong
```

```python
class Solution:
    def searchRange(self, nums: List[int], target: int) -> List[int]:
        # Corner case
        if (nums == None or len(nums) == 0): 
            return [-1, -1]

        def firstPosition(nums, target):
            left = 0
            right = len(nums) - 1
            mid = 0

            while(left + 1 < right):
                mid = int(left + (right - left) / 2)
                if nums[mid] < target:
                    left = mid
                else: # If nums[mid] == target, we set right = mid instead of return, because we need to find the fisrt occurrence.
                    right = mid
  
	    # Post processing
            if nums[left] == target:
                return left
            if nums[right] == target:
                return right

            return -1

        def lastPosition(nums, target):
            left = 0
            right = len(nums) - 1
            mid = 0

            while(left + 1 < right):
                mid = int(left + (right - left) / 2)
                if nums[mid] > target:
                    right = mid
                else: # If nums[mid] == target, we set left = mid instead of return, because we need to find the last occurrence.
                    left = mid
  
	    # Post processing, we need to check nums[right] first
            if nums[right] == target:
                return right
            if nums[left] == target:
                return left

            return -1

        left = firstPosition(nums, target) # Find the first occurrence 
        if left == -1: # if we didn't find any element equals to the target, return {-1, -1}
            return [-1, -1]
        right = lastPosition(nums, target) # Find the last occurrence

        return [left, right]

# Tong
```
