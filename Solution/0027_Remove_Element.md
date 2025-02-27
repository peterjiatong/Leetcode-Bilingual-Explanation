# Remove Element / 移除元素

Leetcode: https://leetcode.com/problems/remove-element/description/

中文力扣：https://leetcode.cn/problems/remove-element/description/

## Solution: Two Pointers / 双指针

I used the two-pointer approach (moving towards each other) for this problem. whenever `nums[left]` equals `val` and `nums[right]` does not equal `val`, assign `nums[left] = nums[right]`. Since the problem requires in-place modification and does not care about the values of elements after index k in the modified array, there is no need to modify the `nums[right]` values, value of `right` should be updated immediately after modifying nums[left] to avoid mistakes

When using while to modify the right boundary, make sure to check whether `right` is greater than or equal to 0 in the termination condition

本题我使用双指针相向而行遍历, 每当 `nums[left]`等于 `val`，且 `nums[right]`不等于 `val`时，让 `nums[left] = nums[right]`， 由于题目要求原地操作，且不在乎修改后的数组下标 `k`后的元素的值，我们不需要对右侧的值做任何修改，为了不影响判断，在更改 `nums[left]`之后，需要立即更新 `right`一次

在使用 `while`对右边界进行修改时，注意需要在终止条件中判断 `right`是否大于等于0

Java

```java
class Solution {
    public int removeElement(int[] nums, int val) {
        int left = 0;
        int right = nums.length - 1;

        while (right >= 0 && nums[right] == val){
            right --;
        }

        while (left <= right){
            if (nums[left] == val){
                nums[left] = nums[right];
                right --;
                while(right >= 0 && nums[right] == val) right --;
            }
  
            left++;
        }

	// at this point, right is indicate the position of first non-val value, and left = right + 1 is the answer
        return left;
    }
}
```

Python

```python
class Solution:
    def removeElement(self, nums: List[int], val: int) -> int:
        left = 0
        right = len(nums) - 1

        while right >= 0 and nums[right] == val: 
            right -= 1

        while left <= right:
            if nums[left] == val:
                nums[left] = nums[right]
                right -= 1
                while right >= 0 and nums[right] == val:
                    right -= 1

            left += 1
	# at this point, right is indicate the position of first non-val value, and left = right + 1 is the answer
        return left

```
