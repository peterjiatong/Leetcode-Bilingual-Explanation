# 209. Minimum Size Subarray Sum / 长度最小的子数组

Leetcode: https://leetcode.com/problems/minimum-size-subarray-sum/description/

力扣：https://leetcode.cn/problems/minimum-size-subarray-sum/description/

## Solution：Sliding Window / 滑动窗口

When solving problems that involve finding a continuous subarray, my first instinct is to use the sliding window approach.

Since the problem asks for the minimum length of a subarray whose sum is greater than or equal to the target value, we should record the length as soon as we find a valid subarray and immediately update the left boundary to avoid missing any possible answers.

if we update the right boundary manually each time, there is a risk of going out of bounds. instead, we can use a while looop or for loop to update the right boundary, which reduces the need to worry about boundary conditions (in this problem, using a for loop tends to be slightly faster).

我在看到寻找到连续的子数组问题时会优先想到滑动窗口解法

因为题目要求寻找最小长度的子数组（其之和大于等于目标值`target`），所以每次找到任何满足要求的子数组时，记录其长度后立刻更新左边界，这样才不会遗漏任何可能的答案

如果每次手动更新右边界，可能会出现出界的问题，我们可以使用while或for循环来更新右边界，这样就不需要太过在意会不会出界了（本题使用for循环的运行时间会低一点）

Java

```java
class Solution {
    public int minSubArrayLen(int target, int[] nums) {
        int n = nums.length;
        int left = 0;
        int res = Integer.MAX_VALUE;
        int sumOfSlidingWindow = 0;

        for (int right = 0; right < n; right ++){
            sumOfSlidingWindow += nums[right];
            while (sumOfSlidingWindow >= target){
                if (right - left + 1 < res) res = right - left + 1;
                sumOfSlidingWindow -= nums[left];
                left ++;
            }
        }

        return res == Integer.MAX_VALUE ? 0 : res;
    }
}
```

Python

```python
class Solution:
    def minSubArrayLen(self, target: int, nums: List[int]) -> int:
        res = float('inf')
        n = len(nums)
        left = right = 0
        sum_of_current_window = 0

      	# You can also use while loop here, but it take more time to run
	for right in range(0, n):
            sum_of_current_window += nums[right]

            while sum_of_current_window >= target:
                if right - left + 1 < res:
                    res = right - left + 1
                sum_of_current_window -= nums[left]
                left += 1

        return res if res != float('inf') else 0

```
