# [238.除自身以外数组的乘积](https://leetcode.com/problems/product-of-array-except-self/)

[English Ver.](/Solution/0238_Product_of_Array_Except_Self.md)

## 解法：双边遍历

为了解决找出数组中除当前元素外所有元素的乘积的问题，我们可以将数组人为的分为两部分。一部分在当前元素的左侧，另一部分在右侧。要得到列表中当前元素的值，我们只需要将左侧部分的乘积乘以右侧部分的乘积。

为了做到这一点，我们可以设置一个叫做 ans 的数组。我们首先将 ans[0] 设置为 1。然后我们用在当前索引 i 之前所有元素的乘积来更新 ans[i]。例如，ans[3] 将是 ans[0] * ans[1] * ans[2]。其后，我们从右到左做同样的事情。我们将这个值保留在一个变量中，并用它更新 ans 中的每个元素。

这个解法的时间复杂度是 O(n)，空间复杂度是 O(n) 或 O(1)。

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
