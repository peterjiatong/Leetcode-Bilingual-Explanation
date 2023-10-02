# [252. 会议室](https://leetcode.com/problems/meeting-rooms/)

[English Ver.](/Solution/0252_Meeting_Rooms.md)

## 解法：排序法

通过对给定数组`intervals`的每个区间的第一个元素进行排序。然后，检查第二个元素是否小于下一个区间的第一个元素，以确保我们是否可以参加所有会议。

此解决方案的时间复杂度为 `O(n log n)`，空间复杂度为 `O(1)`。

Java 解法:

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

Python 解法:

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
