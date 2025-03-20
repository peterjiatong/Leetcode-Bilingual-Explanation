# Squares of a Sorted Array / 有序数组的平方

leetcode: https://leetcode.com/problems/squares-of-a-sorted-array/description/

中文力扣： https://leetcode.cn/problems/squares-of-a-sorted-array/description/

## Solution: Two Pointers / 双指针

Since the given array `nums` is already sorted, we know that the squared values of the non-negative part will also be sorted, so we only need to process the negative part.

My initial idea was to first find the boundary between the negative and non-negative parts, then traverse the non-negative part from left to right and traversing the negative part in reverse from right to left, recording the smaller absolute value each time.

However, I realized that we can reverse this approach by traversing from outside-in, so we do not need to check for out-of-bounds conditions since we only iterate through n elements.

因为给定数组 `nums`本身是有序的，所以我们知道数组的非负数部分的平方一定也是有序的，我们只需要处理数组的负数部分即可

笔者的第一想法是先找到负数和非负数部分的边界，然后将非负数部分从左至右按顺序遍历，将负数部分从右至左按逆序遍历，每次记录绝对值较小的数字

但我发现我们可以将上述思路翻转，从两端向中间遍历，这样就不需要判断是否出界，因为我们只会遍历n个元素

Java


Python

```python
# traverse inside-out
class Solution:
    def sortedSquares(self, nums: List[int]) -> List[int]:
        left = 0
        right = 0
        for i in range(len(nums)):
            if nums[i] < 0:
                left = i
            else:
                break
        right = left + 1

        res = []
  
	# need a while loop
        while left >= 0 or right < len(nums):
            if left < 0:
                res.append(nums[right] * nums[right])
                right += 1
            elif right >= len(nums):
                res.append(nums[left] * nums[left])
                left -= 1
            elif abs(nums[right]) > abs(nums[left]):
                res.append(nums[left] * nums[left])
                left -= 1
            else:
                res.append(nums[right] * nums[right])
                right += 1

        return res
```

```python
# from edge to inside, no need to worry about boundaries anymore
class Solution:
    def sortedSquares(self, nums: List[int]) -> List[int]:
        left = 0
        right = len(nums) - 1

        res = [0] * len(nums)

        for i in range(len(nums) - 1, -1, -1):
            if abs(nums[left]) > abs(nums[right]):
                res[i] = (nums[left] * nums[left])
                left += 1
            else:
                res[i] = (nums[right] * nums[right])
                right -= 1

        return res

```
