# [11. 盛最多水的容器](https://leetcode.com/problems/container-with-most-water/)

[English Ver.](/Solution/0011_Container_With_Most_Water.md)

## 解法1：暴力法（超时）

此解决方案比较了给定数组 'height' 中的每一对可能组合。由于嵌套循环，时间复杂度是 O(n^2)，空间复杂度是 O(1)，因为只使用了常数额外空间。"

Java解法

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

Python解法

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

## 解法2：双指针

设置两个指针，left 和 right，分别初始化为 0 和 height.length -1。由于面积值取决于较低的边界，为了找到 left 和 right 指针之间的最大面积值，我们应该移动当前值较小的那个指针。当 left 和 right 指针重叠时停止。如果 left 值等于 right 值，那么我们可以移动任意一个，因为较低的边界的值不会改变。

此解决方案的时间复杂度为 `O(n)`，因为只了进行一次遍历，空间复杂度为 `O(1)`。

Java解法

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

Python解法

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
