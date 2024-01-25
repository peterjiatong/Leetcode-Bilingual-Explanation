# Meeting Rooms II / 会议室 II

Leetcode: https://leetcode.com/problems/meeting-rooms-ii/

中文力扣：https://leetcode.cn/problems/meeting-rooms-ii/

## Description / 题目描述

Given an array of meeting time intervals `intervals` where `intervals[i] = [starti, endi`, return  *the minimum number of conference rooms required* .

给你一个会议时间安排的数组 `intervals` ，每个会议时间都会包括开始和结束的时间 `intervals[i] = [starti, endi]` ，返回 *所需会议室的最小数量* 。

## Solution: PriorityQueue / 优先队列

First, sort the given array `intervals`, prioritizing the comparison of the first number in each interval. After sorting, create a priority queue `pq` to record the end times of each interval (the priority queue sorts numbers in ascending order by default).

Iterate through the given array `intervals`:

1. If the start time of the current interval is less than the smallest end time in `pq`, it indicates that a new meeting room is needed, so add the end time of the current interval to `pq`.
2. Otherwise, it means that a new meeting room is not needed for the current interval (the current interval can use the meeting room of a previously completed interval). Remove the smallest end time from `pq` and add the end time of the current interval to `pq`.

After the iteration, return the length of `pq`. The time complexity of this algorithm is `O(n log n)` due to the use of a sorting algorithm.

先对给定数组`intervals`排序，排序时优先比较区间中的第一个数。排序完成后，创建一个优先队列`pq`由于记录每个区间的结束时间(由于使用优先队列，`pq`中的数会默认为升序排列)。

遍历给定数组`intervals`：

1. 若当前区间的开始时间小于`pq`中的最小的结束时间，则表明我们需要一个新的会议室，将当前区间的结束时间加入`pq`
2. 反之，证明当前区间的不需要一个新的会议室(当前区间可以使用上一个已经完成的区间使用的会议室)，将`pq`中的最小的结束时间移除队列，将当前区间的结束时间加入`pq`

遍历完成后，返回`pq`的长度即可，此算法时间复杂度为`O(n log n)`， 因为使用了排序算法。

Java

```java
class Solution {
    public int minMeetingRooms(int[][] intervals) {
        if (intervals.length == 0) return 0;

        Arrays.sort(intervals, (a, b) -> Integer.compare(a[0], b[0]));

        PriorityQueue<Integer> pq = new PriorityQueue<>(); // Integer PriorityQueue in Java will sort elements in ascending order by default

        pq.add(intervals[0][1]);
        for (int i = 1; i < intervals.length; i++){
            if (intervals[i][0] >= pq.peek()) pq.poll();
            pq.add(intervals[i][1]);
        }
  
        return pq.size();
    }
}

```

Python

```python
class Solution:
    def minMeetingRooms(self, intervals: List[List[int]]) -> int:
        if len(intervals) == 0:
            return 0
  
        intervals.sort()
        pq = []
	# Since python does not have a build-in PriorityQueue, we can use a normal list and modify it with heapq to do the same thing
        heapq.heappush(pq, intervals[0][1])
        for i in range(1, len(intervals)):
            if intervals[i][0] >= pq[0]:
                heapq.heappop(pq)
            heapq.heappush(pq, intervals[i][1])

        return len(pq)

```
