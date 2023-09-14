# [57. Insert Interval](https://leetcode.com/problems/insert-interval/)

中文版本

## Solution

We can traverse the 

```python
# Solution 1 (Single Pass) | O(n) time, O(n) space
class Solution:
    def insert(self, intervals: List[List[int]], newInterval: List[int]) -> List[List[int]]:
        s, e = newInterval[0], newInterval[1]

        # Create 2 lists to hold intervals strictly before and strictly after the newInterval
        left, right = [], []

        # Traverse the list of intervals and either add them to the left/right lists or merge overlapping ones
        for i in intervals:
            if i[1] < s:
                # If the interval is strictly before newInterval, add it to the left half
                left += [i]
            elif i[0] > e:
                # If the interval is strictly after newInterval, add it to the right half
                right += [i]
            else:
                # If the interval overlaps with newInterval, merge them by updating newInterval
                s = min(s, i[0])
                e = max(e, i[1])

        # Return the new interval list
        return left + [[s, e]] + right
```
