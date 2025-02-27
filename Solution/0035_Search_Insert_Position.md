# Search Insert Position / 搜索插入位置

Leetcode: https://leetcode.com/problems/search-insert-position/

中文力扣：https://leetcode.cn/problems/search-insert-position/

## Solution: Binary Search / 二分搜索

When performing a binary search on the given array `nums`, there are four possible cases for the position of `target`:

1. target exists in the array (nums[mid] equals target)
2. target does not exist in the array
   1. target should be inserted before the entire array
   2. target should be inserted at some position within the array
   3. target should be inserted after the entire array

Should consider whether boundary checks are needed after the search is completed

对给定数组 `nums`进行二分搜索时，`target`的位置共有4种情况：

1. target 存在于数组中（nums[mid] == target)
2. target 不存在于数组中：
   1. target应该插入在整个数组之前
   2. target应该插入在数组中的某个位置
   3. target应该插入在整个数组之后

本题应该考虑在搜索结束后是否需要额外判断边界

Java

```java
// with boundary checks
class Solution {
    public int searchInsert(int[] nums, int target) {
        int left = 0;
        int right = nums.length - 1;

        while(left + 1 < right){
            int mid = left + (right - left) / 2;
            if (nums[mid] == target) return mid;
            else if (nums[mid] > target) right = mid;
            else left = mid;
        }

        if (nums[left] >= target) return left;
        if (nums[right] >= target) return right;
        return right + 1;
    }
}

```

```java
// without boundary checks
class Solution {
    public int searchInsert(int[] nums, int target) {
        int left = 0;
        int right = nums.length - 1;
        int middle = 0;
     
        while (left <= right){
            middle = left + ((right - left) >> 1);
            if (nums[middle] < target) left = middle + 1;
            else if (nums[middle] > target) right = middle - 1;
            else return middle;
        }

        return right + 1;
    }
}
```

Python

```python
# without boundary checks
class Solution:
    def searchInsert(self, nums: List[int], target: int) -> int:
        left = 0
        right = len(nums) - 1

        while left + 1 < right:
            mid = left + (right - left) // 2
            if nums[mid] == target:
                return mid
            elif nums[mid] > target:
                right = mid
            else:
                left = mid
  
        if nums[left] >= target:
            return left
        elif nums[right] >= target:
            return right
        return right + 1
  
```

```python
# without boundary checks
class Solution:
    def searchInsert(self, nums: List[int], target: int) -> int:
        left = 0
        right = len(nums) - 1

        while left <= right:
            mid = left + (right - left) // 2
            if nums[mid] > target:
                right = mid - 1
            elif nums[mid] < target:
                left = mid + 1
            else:
                return mid
  
        return right + 1
```
