# [252. Meeting Rooms](https://leetcode.com/problems/meeting-rooms/)

[中文版本](/Solution_CN/0252_Meeting_Rooms_CN.md)

## Solution: Sorting

Sort the given array `intervals` by the first element of each interval. Then, simply check whether the second element is smaller than the first element of the next interval to make sure if we can attend all meetings.

This solution has an `O(n log n)` time complexity, and an `O(1)` space complexity.

Java Solution:

```java
class Solution {
    public boolean canAttendMeetings(int[][] intervals) {
        Arrays.sort(intervals, (a, b) -> Integer.compare(a[0], b[0])); // Sort given array
        for(int i = 0; i < intervals.length - 1; i++){ // Make sure it does not go out of bound
            if (intervals[i][1] > intervals[i+1][0]) return false;
        }
        return true;
    }
}

// Tong, 02/10/2023
```

Python Solution:

```python
class Solution:
    def canAttendMeetings(self, intervals: List[List[int]]) -> bool:
        intervals.sort()
        for i in range(len(intervals) - 1): # Make sure it does not go out of bound
            if intervals[i][1] > intervals[i+1][0]:
                return False
  
        return True

# Tong, 02/10/2023
```
