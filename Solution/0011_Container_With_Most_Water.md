# [11. Container With Most Water](https://leetcode.com/problems/container-with-most-water/)

[中文版本](/Solution_CN/0011_Container_With_Most_Water_CN.md)

## Solution 1: Brute Force(Time Limit Exceeded)

This solution simply just compares every possible pair of the given array height, time complexity is `O(n^2)` because we put a loop inside of a loop, space complexity is `O(1)` since constant extra space is used.

Java solution

```java
class Solution {
    public int maxArea(int[] height) {
        int max = 0;
        for (int i = 0; i < height.length - 1; i++){
            for (int j = i + 1; j < height.length; j++){
                int temp = Math.min(height[i], height[j]) * (j - i);
                if (temp > max) max = temp;
            }
        }
        return max;
    }
}

// Tong, 9/22/2023
```

Python solution

```python
class Solution:
    def maxArea(self, height: List[int]) -> int:
        max = 0

        for i in range(len(height) - 1):
            for j in range(len(height)):
                temp = min(height[i], height[j]) * (j - i)
                if temp > max: max = temp

        return max

# Tong, 9/22/2023
```

## Solution 2: Two Pointers

We set up two pointers, left and right, initializing them to 0 and height.length -1, respectively. Since the area value is depends on the lower bound, to find the maximum area value between the left and right pointers, we should move the pointer with the lesser value. We stop when the left and right pointers overlap. If the left value equals the right value, then we can move either one, as the lower bound will not change.

This solution has a time complexity of `O(n)` due to a single pass and a space complexity of `O(1)`.

Java Solution

```java
class Solution {
    public int maxArea(int[] height) {
        int left = 0;
        int right = height.length - 1;
        int max = 0;

        while (left < right){
            int temp = Math.min(height[left], height[right]) * (right - left); # Count current area
            if (temp > max) max = temp; // Update max

	    // Update pointers
            if (height[left] > height[right]){
                right --;
            }else {
                left ++;
            }
        }
  
        return max;
    }
}
```

Python Solution

```python
class Solution:
    def maxArea(self, height: List[int]) -> int:
        left = 0
        right = len(height) - 1
        max = 0

        while left < right:
            temp = min(height[left], height[right]) * (right - left) # Count current area
            if temp > max: max = temp

            if height[left] > height[right]: # Update pointers
                right -= 1
            else:
                left += 1

        return max

# Tong, 9/22/2023
```
