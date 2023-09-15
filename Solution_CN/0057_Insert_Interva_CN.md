# [57.插入区间](https://leetcode.com/problems/insert-interval/)

[English Version](/Solution/0057_Insert_Interval.md)

## Solution

遍历以找到 newInterval 的正确位置，使用一个列表以存储正确答案。在 for 循环过程中，可能会出现三种情况：

1. intervals[i][1] 小于 newInterval[0]：在这种情况下，我们正在查看的区间小于 newInterval，我们将这个区间添加到答案列表中即可。
2. newInterval[1] 小于 intervals[i][0]：我们正在查看的区间大于 newInterval，在这种情况下，我们将 newInterval 添加到答案列表中，然后添加正在查看的区间。
3. 不符合以上任意情况时，表明区间之间有重叠发生，我们需要修改 newInterval 的起始和结束值以追踪到正确答案。

Python

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


#Kevin
```

Java

```java
class Solution {
    public int[][] insert(int[][] intervals, int[] newInterval) {
        List<int[]> ans = new ArrayList<>();
	// Keep track the start and end value
        int start = newInterval[0];
        int end = newInterval[1];
	// Keep track if we found out the answer
        boolean noAns = true;

        for (int[] interval : intervals) {
            if (end < interval[0]) {
                if (noAns) { //if answer not found, insert answer here
                    ans.add(new int[]{start, end});
                    noAns = false;
                }
                ans.add(interval);
            } else if (interval[1] < start) {
                ans.add(interval);
            } else { // Update start and end value
                start = Math.min(start, interval[0]);
                end = Math.max(end, interval[1]);
            }
        }

	// If newInterval[0] is greater than every elements in intervals, we need to add it on the end
        if (noAns) {
            ans.add(new int[]{start, end});
        }

	// Return a int[][]
        return ans.toArray(new int[ans.size()][]);
    }
}

//Tong, 9/14/2023
```
