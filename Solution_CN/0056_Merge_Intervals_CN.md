# [56. 合并区间](https://leetcode.com/problems/merge-intervals/)

[English Ver.](/Solution/0056_Merge_Intervals.md)

## 解法： 排序

在合并给定的区间之前，我们需要对它们进行排序，因为题中的给定区间不是有序的。排序之后，我们设置两个变量，`left` 和 `right`，来跟踪我们当前正在处理的区间。然后，我们遍历给定的区间：

1. 如果当前区间的起始点（`interval[0]`）大于 `right`，这意味着正在处理的区间没有重叠发生。在这种情况下，`[left, right]` 是一个有效的区间，我们可以将其添加到答案列表中。然后我们需要将 `left` 和 `right` 更新为当前区间的值。
2. 如果当前区间的起始点（`interval[0]`）小于或等于 `right`，这意味着 `[left, right]` 和当前区间之间存在重叠。我们需要将它们合并在一起。

在循环结束后，确保再次将 `[left, right]`加入答案，因为最后一个合并的有效区间尚未添加到我们的答案列表中。

该解决方案的时间复杂度为 `O(n log n)`，因为排序需要 `O(n log n)` 的时间，循环需要 `O(n)` 的时间。空间复杂度为 `O(n)`，因为答案列表的大小可能与给定的区间一样大。

Java

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

// Tong, 9/20/2023
```

Python

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

# Tong, 9/20/2023
```
