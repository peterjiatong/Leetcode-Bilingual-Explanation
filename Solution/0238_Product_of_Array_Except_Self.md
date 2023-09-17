# [238. Product of Array Except Self](https://leetcode.com/problems/product-of-array-except-self/)

[中文版本](/Solution_CN/0238_Product_of_Array_Except_Self_CN.md)

## Solution : Two Side Traverse

To solve the problem of finding the product of every element in an array except for the current one, we can split the array into two parts. One part is on the left of the current index and the other part is on the right. To get the value at the current index, we just need to multiply the product of the left part by the product of the right part.

To do this, we can set up an array called ans. We start by setting ans[0] to 1. Then we update ans[i] with the product of all elements that come before the current index i. For example, ans[3] would be ans[0] * ans[1] * ans[2]. Next, we do the same thing from right to left. We keep this value in a variable and update each element in ans with it.

This solution has an O(n) time complexity and an O(n) or O(1) space complexity.

Java

```java
class Solution {
    public int[] productExceptSelf(int[] nums) {
        int[] ans = new int[nums.length];
        int cur = 1; // cur = 1 makes sure that we initialize ans[0] to 1

        for (int i = 0; i < nums.length; i++){
            ans[i] = cur;
            cur = cur * nums[i]; // Update cur equals to the product of all elements that come before the current index i.
        }

        cur = 1; // Reset cur, instead of setting up a new array, by reuse cur, we can limit space complexity to O(1)
        for (int i = 0; i < nums.length; i++){
            int curIndex = nums.length - 1 - i; // Track the index from right to left
            ans[curIndex] = ans[curIndex] * cur; // Now ans[i] is the product of part on the left of index i and on the right of index i
            cur = cur * nums[curIndex];	// Calculate cur the other way around
        }

        return ans;
    }
}

//Tong, 9/16/2023
```

Python

```python
class Solution:
    def productExceptSelf(self, nums: List[int]) -> List[int]:
        ans = [0] * len(nums)
        cur = 1 # cur = 1 makes sure that we initialize ans[0] to 1
        for i in range(len(nums)):
            ans[i] = cur
            cur = cur * nums[i] # Update cur equals to the product of all elements that come before the current index i.

        cur = 1 # Reset cur, instead of setting up a new array, by reuse cur, we can limit space complexity to O(1)
        for i in range(len(nums)):
            ans[-(i + 1)] = ans[-(i + 1)] * cur # Now ans[i] is the product of part on the left of index i and on the right of index i
            cur = cur * nums[-(i + 1)]

        return ans

#Tong, 9/16/2023
```
