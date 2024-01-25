# Employee Free Time / 员工空闲时间

Leetcode: https://leetcode.com/problems/employee-free-time/

中文力扣: https://leetcode.cn/problems/employee-free-time/

## Description / 题目描述

We are given a list `schedule` of employees, which represents the working time for each employee.

Each employee has a list of non-overlapping `Intervals`, and these intervals are in sorted order.

Return the list of finite intervals representing **common, positive-length free time** for *all* employees, also in sorted order.

(Even though we are representing `Intervals` in the form `[x, y]`, the objects inside are `Intervals`, not lists or arrays. For example, `schedule[0][0].start = 1`, `schedule[0][0].end = 2`, and `schedule[0][0][0]` is not defined).  Also, we wouldn't include intervals like [5, 5] in our answer, as they have zero length.

给定员工的 `schedule` 列表，表示每个员工的工作时间。

每个员工都有一个非重叠的时间段  `Intervals` 列表，这些时间段已经排好序。

返回表示 *所有 *员工的 **共同，正数长度的空闲时间 **的有限时间段的列表，同样需要排好序。

## Solution: Sorting / 排序

The solution approach for this one is similar to LeetCode problems 56 and  57, ([56.Merge Intervals ](/Solution/0056_Merge_Intervals.md)/ [57. Insert Interval](/Solution/0057_Insert_Interval.md)).  First, we place all employee work intervals into a single list. Then, we sort the elements in this list. For sorting, we prioritize by comparing the start of the intervals and then the end.

After sorting, we begin to compare the intervals. If the start time of an interval is greater than the end time of the previous interval, it indicates that the time between these two intervals is a free time period. Since we have already sorted all intervals, we don't need to check for overlapping intervals.

The time complexity of this algorithm is `O(n log n)`.

此题解法思路和力扣56，57题相似([56.合并区间](/Solution/0056_Merge_Intervals.md) / [57.插入区间](/Solution/0057_Insert_Interval.md))，我们先将所有员工的工作区间放在同一个列表中，之后对列表中的元素进行排序，排序时，优先比较区间的start，再比较end。

排序后，我们开始对区间进行比较，如果某个区间的开始时间大于上一个区间的结束时间，就说明这两个区间中间的时间就是空闲时间，又因为我们已经先对所有区间进行了排序，所以我们不需要考虑区间重合的问题。

此算法时间复杂度为 `O(n log n)`

Java

```java
class Solution {
    public List<Interval> employeeFreeTime(List<List<Interval>> schedule) {
        ArrayList<Interval> ans = new ArrayList<>();
        ArrayList<Interval> allInterval = new ArrayList<>();
        for (List<Interval> intervals : schedule){
            for (Interval interval : intervals){
                allInterval.add(interval);
            }
        }

        Collections.sort(allInterval, (a, b) -> {
            if (Integer.compare(a.start, b.start) != 0) {
                return Integer.compare(a.start, b.start);
            }
            return Integer.compare(a.end, b.end);
        });

        for (int i = 1; i < allInterval.size(); i++){
            if (allInterval.get(i).start > allInterval.get(i - 1).end){
                ans.add(new Interval(allInterval.get(i - 1).end, allInterval.get(i).start));
            }
        }

        return ans;  
    }
}

```

Python

```python
class Solution:
    def employeeFreeTime(self, schedule: '[[Interval]]') -> '[Interval]':
        allInterval = []
        ans = []
        for intervals in schedule:
            for interval in intervals:
                allInterval.append(interval)

        allInterval.sort(key=lambda interval: (interval.start, interval.end))

        if len(allInterval) == 1:
            return []

        for i in range(1, len(allInterval)):
            if allInterval[i].start > allInterval[i - 1].end:
                ans.append(Interval(allInterval[i - 1].end, allInterval[i].start))

        return ans

```
