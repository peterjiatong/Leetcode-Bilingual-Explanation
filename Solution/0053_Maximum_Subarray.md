# [Maximum Subarray](https://leetcode.com/problems/maximum-subarray/)

## Solution

**Solution 1: Sliding Window**

The solution employs the sliding window approach to find the maximum subarray sum within the given list of integers (nums). By iterating through the list, the algorithm maintains two variables: sum and maxSum. The sum tracks the running sum of elements, and the maxSum stores the maximum subarray sum encountered.

During each iteration, the algorithm updates the sum by either extending the previous subarray sum (sum + val) or starting a new subarray from the current value (val). The maxSum is updated whenever the current sum exceeds the existing maxSum.

The approach effectively identifies the contiguous subarray with the largest sum and returns the result.

Time Complexity: O(n)
Space Complexity: O(1)

### Python
```python
class Solution:
    def maxSubArray(self, nums: List[int]) -> int:
        sum = 0
        maxSum = nums[0]

        # Use sliding window approach to find the max sum
        for val in nums:
            # New sum either includes previous values (sum + val) or starts from current value (val). Update maxSum if current sum is greater
            sum = max(val, sum + val)
            maxSum = max(maxSum, sum)

        return maxSum
```