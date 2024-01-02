# Insert Interval / 插入区间

Leetcode: https://leetcode.com/problems/insert-interval/

中文力扣: https://leetcode.com/problems/insert-interval/

## Solution: Linear approach / 线性解法

Create a List `ans` to record the answer. Iterate through the given `intervals` once, and during the iteration, there are 3 possible cases:

1. `newInterval[1] < intervals[i][0]`: This is the simplest case, where you only need to add `newInterval` to `ans`, followed by adding the current `interval` to `ans`.
2. `intervals[i][1] < newInterval[0]`: In this case, `newInterval` does not overlap with the current interval and is after the current interval. Just add the current `interval` to `ans`, and then continue to the next interval.
3. Otherwise, then `newInterval` overlaps with the current interval, and the current interval needs to be merged into `newInterval`.

After the iteration, `ans` will be the merged interval result. It is important to note that `newInterval` might not have been added to `ans` in case 3, so you should manually add it after exiting the iteration.

The time complexity of this solution is `O(n)`.

创建一个List `ans`用于记录答案，遍历给定 `intervals`一次， 遍历途中，有3种可能出现的情况：

1. `newinterval[1] < intervals[i][0]`：这种情况是最简单的情况，只需将 `newinterval`添加至 `ans`即可，之后将当前的 `interval`也添加至 `ans`
2. `intervals[i][1] < newInterval[0]`： 这种情况说明 `newinterval`与当前区间不重合且在当前区间之后，无需做任何改变，将当前的 `interval`添加至 `ans后，`继续遍历下一个区间即可
3. 若以上两种条件都不满足，说明 `newinterval`与当前区间有重合，需要将当前区间合并至 `newinterval`

遍历之后，`ans`就是合并后的区间结果，需要注意的是，进入条件3后，`newinterval`可能没有被加入至`ans`，跳出遍历后需要手动天剑

此解时间复杂度为 `O(n)`


Java:

```java
class Solution {
    public int[][] insert(int[][] intervals, int[] newInterval) {
        List<int[]> ans = new ArrayList<>();
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

        return ans.toArray(new int[ans.size()][]);
    }
}

```


Python:

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
