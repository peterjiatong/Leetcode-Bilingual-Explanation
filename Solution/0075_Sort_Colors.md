# [75. Sort Colors](https://leetcode.com/problems/sort-colors/)

[中文版本](/Solution_CN/0075_Sort_Colors_CN.md)

## Solution 1: 2-pass Counting Sort

Traverse the given array to count the occurrences of 0, 1, and 2, and store these counts in a bucket where the index represents the number and the value represents the count of occurrences, functioning similarly to a dictionary. Then, perform a second pass to modify 'nums' in order, based on the values in the bucket.

This solution has a time complexity of `O(n)` and a space complexity of `O(3)`.

Java solution

```java
class Solution {
    public void sortColors(int[] nums) {
        int[] bucket = {0,0,0};

        for (int num : nums){
            bucket[num] ++;
        }

	// Count represent the current number, cumulative represent the current index
        int count = 0;
        int cumulative = 0;

        for (int value : bucket){
            for (int i = 0; i < value; i++){
                nums[cumulative] = count;
                cumulative ++;
            }
            count ++;
        }
    }
}

// Tong, 9/21/2023
```

Python solution

```python
class Solution:
    def sortColors(self, nums: List[int]) -> None:
        """
        Do not return anything, modify nums in-place instead.
        """
        bucket = [0,0,0]

        for num in nums:
            bucket[num] += 1

      	# Count represent the current number, cumulative represent the current index
	count = 0
        cumulative = 0

        for num in bucket:
            for _ in range(num):
                nums[cumulative] = count
                cumulative += 1
            count += 1

# Tong, 9/21/2023
```

## Solution 2: Two Pointers, One Pass

The idea behind this solution is to traverse the array only once. If the value at the current index == 0, swap it with the value at the left pointer. Conversely, if the value at the current index == 2, swap it with the value at the right pointer. If the value at the current index == 1, we ignore it. Don’t forget to update the pointers after each swap.

This solution has an `O(n)` time complexity as we perform the operation in one pass, which is significantly faster than solution 1. The space complexity is `O(1)`, as only a constant space is used for the swap.

Java solution

```java
class Solution {
    public void sortColors(int[] nums) {
        int left = 0;
        int right = nums.length - 1;
        int curr = 0;

        while(curr <= right){
            if (nums[curr] == 0){ // Make sure every element get checked
                swap(nums, curr, left);
		// Update both curr and left because we already know that from index 0 to left are all 0s
                curr ++;
                left ++;
            }else if (nums[curr] == 2){
                swap(nums, curr, right);
		// Only update right because we can't make sure what happens on the left part
                right --;
            }else {
                curr ++;
            }
        }
}

// Tong, 9/21/2023
    public void swap(int[] nums, int p1, int p2){
        int temp = nums[p1];
        nums[p1] = nums[p2];
        nums[p2] = temp;
    }
}
```

Python solution

```python
class Solution:
    def sortColors(self, nums: List[int]) -> None:
        """
        Do not return anything, modify nums in-place instead.
        """
        left = 0
        right = len(nums) - 1
        curr = 0

        def swap(nums: List[int], p1: int, p2: int):
            temp = nums[p1]
            nums[p1] = nums[p2]
            nums[p2] = temp

        while(curr <= right): # Make sure every element got checked
            if nums[curr] == 0:
                swap(nums, curr, left)
		# Update both curr and left because we already know that from index 0 to left are all 0s
                curr += 1
                left += 1
            elif nums[curr] == 2:
                swap(nums, curr, right)
		# Only update right because we can't make sure what happens on the left part
                right -= 1
            else:
                curr += 1

# Tong, 9/21/2023
```
