# [57. Insert Interval](https://leetcode.com/problems/insert-interval/)

[中文版本](/Solution_CN/0057_Insert_Interva_CN)

## Solution

Traverse to find the correct position for newInterval, set up a list to store correct answer, during the for loop, 3 cases can show up:

1. intervals[i][1] < newInterval[0]: in this case, interval we are looking at is less than the newInterval, we add interval into the answer list and move on.
2. newinterval[1] < interval[i][0]: interval we are looking at is greater than the newInterval, in this case, we add newInterval to the answer list, and than add interval.
3. otherwise, we know there is a overlap occurs, we need to modify start and end value of the newInterval in order to track the correct answer.

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

Java:

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

//Tong
```
