# Meeting Rooms / 会议室

Leetcode: https://leetcode.com/problems/meeting-rooms/description/

中文力扣：https://leetcode.cn/problems/meeting-rooms/description/

## Description / 题目描述

Given an array of meeting time `intervals` where `intervals[i] = [starti, endi]`, determine if a person could attend all meetings.

给定一个会议时间安排的数组 `intervals` ，每个会议时间都会包括开始和结束的时间 `intervals[i] = [starti, endi]` ，请你判断一个人是否能够参加这里面的全部会议。

## Solution: Sorting / 排序法

First, sort the given array `intervals`, with priority given to comparing the first element of each interval. Then, check if the second number of each interval overlaps with the first number of next element.

先将给定数组 `intervals`排序，排序时优先比较区间中的第一个数。之后检查每个区间的第二个数和下一个区间的第一个数是否重合。

因为使用了排序算法，此解法的时间复杂度为 `O(n log n)`

Java:

```java
class Solution {
    public boolean canAttendMeetings(int[][] intervals) {
        Arrays.sort(intervals, (a, b) -> Integer.compare(a[0], b[0]));
        for(int i = 0; i < intervals.length - 1; i++){
            if (intervals[i][1] > intervals[i+1][0]) return false;
        }
        return true;
    }
}

```

Python:

```python
class Solution:
    def canAttendMeetings(self, intervals: List[List[int]]) -> bool:
        intervals.sort()
        for i in range(len(intervals) - 1):
            if intervals[i][1] > intervals[i+1][0]:
                return False
  
        return True

```
