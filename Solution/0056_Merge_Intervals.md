# Merge Intervals / 合并区间

Leetcode: https://leetcode.com/problems/merge-intervals/

中文力扣：https://leetcode.cn/problems/merge-intervals/

## Description / 题目描述

Given an array of `intervals` where `intervals[i] = [starti, endi]`, merge all overlapping intervals, and return  *an array of the non-overlapping intervals that cover all the intervals in the input* .

以数组 `intervals` 表示若干个区间的集合，其中单个区间为 `intervals[i] = [starti, endi]` 。请你合并所有重叠的区间，并返回 *一个不重叠的区间数组，该数组需恰好覆盖输入中的所有区间* 。

## Solution: Sorting + Linear approach / 排序 + 线性解法

Before merging, note that the given array `intervals` is unordered. We can sort them first, with priority given to comparing the first element of each interval.

Let's define three variables: `ans` to record the answer, and `left` and `right` to track the processing interval's left and right boundaries. We iterate through the given `intervals` once, during this iteration, there are two possible scenarios:

1. If the left boundary of the current interval is greater than `right`, it indicates that the interval represented by `[left, right]` does not overlap with the current interval and is smaller than the current interval. We add `[left, right]` to `ans` and then update `[left, right]` to the current interval's boundaries.
2. If the left boundary of the current interval is less than or equal to `right`, it means that the interval represented by `[left, right]` overlaps with the current interval, and we need to merge them. Since the given `intervals` array is pre-sorted before iteration, we only need to update `right` to the larger boundary.

After the iteration, make sure to check if the last interval has been added to `ans`.

Since sorting algorithm is used, the time complexity of this solution is at least `O(n log n)`.

在合并之前，请注意给定数组 `intervals`是无序的，我们可以先将他们排序，排序时优先比较第一个数。

创建三个变量： `ans`用于记录答案，`left`和 `right`用于记录当前处理的区间的左右边界。遍历给定 `intervals`一次， 遍历途中，有2种可能出现的情况：

1. 如果当前所处的区间的左边界大于 `right`，说明 `[left, right]`所代表的区间和当前区间不重合且比当前区间小，将 `[left, right]` 加入ans，之后更新 `[left, right]`为当前区间的左右边界
2. 如果当前所处的区间的左边界小于或等于 `right`， 说明 `[left, right]`所代表的区间和当前区间有重合，我们需要合并两个区间，因为在遍历前有对给定数组 `intervals`进行预处理排序，所以我们只需要更新`right`为更大的边界即可

遍历完成后，需要检查最后一个区间是否添加至 `ans`

因使用了排序，此解法时间复杂度最低为 ` O(n log n)`


Java:

```java
class Solution {
    public int[][] merge(int[][] intervals) {
	// Sort since given intervals is not in order
        Arrays.sort(intervals, (a, b) -> Integer.compare(a[0], b[0]));
        List<int[]> ans = new ArrayList<>();
        int left = intervals[0][0];
        int right = intervals[0][1];

        for (int i = 1; i < intervals.length; i++) {
            if (intervals[i][0] > right) {
                ans.append([left, right])
                ans.add(new int[]{left, right});
                left = intervals[i][0];
                right = intervals[i][1];
            } else {
		// left = Math.min(left, intervals[i][0])
                right = Math.max(right, intervals[i][1]);
            }
        }

        ans.add(new int[]{left, right});
        return ans.toArray(new int[ans.size()][]);
    }
}

```

Python:

```python
class Solution:
    def merge(self, intervals: List[List[int]]) -> List[List[int]]:
        # Sort since given intervals is not in order
        intervals.sort()
        left = intervals[0][0]
        right = intervals[0][1]
        ans = []

        for i in range(1, len(intervals)):
            if intervals[i][0] > right:
                ans.append([left, right])
                left = intervals[i][0]
                right = intervals[i][1]
            else:
                # left = min(left, intervals[i][0])
                right = max(right, intervals[i][1])

        ans.append([left, right])
        return ans

```
