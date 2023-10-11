# [56. Merge Intervals](https://leetcode.com/problems/merge-intervals/)

[中文版本](/Solution_CN/0056_Merge_Intervals_CN.md)

## Solution: Sorting

Before we merge the given intervals, we need to sort them, as they are not provided in order. After that, we set up two variables, `left` and `right`, to track the intervals we are currently dealing with. Then, we loop over the given intervals:

1. If the current interval's starting point (`interval[0]`) is greater than `right`, it means that there is no overlap occurring. In this case, `[left, right]` is a valid interval, and we can add it to the answer list. Then we need to update `left` and `right` to the values of the current interval.
2. If the current interval's starting point (`interval[0]`) is less than or equal to `right`, it means that there is an overlap between `[left, right]` and the current interval. We need to merge them together.

After the loop, make sure to append `[left, right]` again, as the last merged valid interval has not been added to our answer list.

This solution has a time complexity of ` O(n log n)` because sorting takes `O(n log n)`and looping takes `O(n)`. The space complexity would be `O(n)`, as the answer list may be the same size as the given intervals.

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
            if (intervals[i][0] > right) { // Current interval[0] is greater then right means [left, right] has not overlap with current interval, we can append it to ans and update left and right to current intervals
                ans.append([left, right])
                ans.add(new int[]{left, right});
                left = intervals[i][0];
                right = intervals[i][1];
            } else { // Merge [left, right] with current interval if there's a overlap
                right = Math.max(right, intervals[i][1]);
            }
        }

	// Post-Processing, we need to append left and right again at the end since last merged interval not added
        ans.add(new int[]{left, right});

        return ans.toArray(new int[ans.size()][]);
    }
}

// Tong
```

Python:

```python
class Solution:
    def merge(self, intervals: List[List[int]]) -> List[List[int]]:
        # Sort since given intervals is not in order
        intervals.sort()
        # Initialize left and right
        left = intervals[0][0]
        right = intervals[0][1]
        ans = []

        for i in range(1, len(intervals)):
            # Current interval[0] is greater then right means [left, right] has not overlap with current interval, we can append it to ans and update left and right to current intervals
            if intervals[i][0] > right:
                ans.append([left, right])
                left = intervals[i][0]
                right = intervals[i][1]
            else: # Merge [left, right] with current interval if there's a overlap
                # left = min(left, intervals[i][0])
                right = max(right, intervals[i][1])

        # Post-Processing, we need to append left and right again at the end since last merged interval has not been added
        ans.append([left, right])

        return ans

# Tong
```
