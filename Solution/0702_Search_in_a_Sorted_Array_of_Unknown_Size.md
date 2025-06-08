# 702 Search in a Sorted Array of Unknown Size / 搜索长度未知的有序数组

leetcode: https://leetcode.com/problems/search-in-a-sorted-array-of-unknown-size/description/

力扣：https://leetcode.cn/problems/search-in-a-sorted-array-of-unknown-size/description/

## Solution: Binary Search / 二分搜索

Since we can only access the array using the given `ArrayReader.get()` API and cannot use indices directly, we use a sliding window approach that doubles the search range each time to determine where the target might be. Specifically, we use two integer variables, `left` and `right`, to represent the current search window. If `ArrayReader.get(right) < target`, it means the target is not within the current window (i.e., it lies to the right), so we update `left = right` and `right = right * 2` to expand the search range.

Additionally, since `ArrayReader.get(i)` returns `2^31 - 1` when accessing an invalid index, we know the array consists of valid data followed by an infinite sequence of `2^31 - 1`s. This allows us to apply binary search directly once the window is determined.

This algorithm has a time complexity of `O(log n)`.

因为我们只能通过给定的 `ArrayReader.get() `api来访问数组，无法通过下标来访问数组，所以我们采用滑动窗口的方法每次使搜索范围翻倍来确定target存在的位置：具体做法为使用两个整数变量 `left`和 `right`来表示当前搜索的窗户，若 `ArrayReader.get(right) < target`，则说明 `target`还不在当前窗口内（ `target`在当前窗口的右边），所以让 `left = right`, `right = right * 2`	来扩大窗口的搜索的范围

又因为当访问一个无效下标时，`ArrayReader.get(i)` 返回 ` 2^31^ - 1`， 我们能知道数组的结构一定是 有效数据 后接无数个 `2^31^ - 1`，所以我们在确认窗口后可以直接使用二分搜索

此算法时间复杂度为`O(log n)`

Java

```java
class Solution {
    public int search(ArrayReader reader, int target) {
        // Corner case
        if (reader.get(0) == target) return 0;

        int left = 0;
        int right = 1;
    
        // if reader.get(right) !< target, meaning target must exists in the [left, right]
        while(reader.get(right) < target){
            left = right;
            right *= 2;
        }

        // Binary Search
        while (left <= right) {
            int mid = left + (right - left) / 2;
            if (reader.get(mid) == target) return mid;
            else if (reader.get(mid) > target) right = mid - 1;
            else left = mid + 1;
        }

        return -1;
    }
}
```

Python

```python
# """
# This is ArrayReader's API interface.
# You should not implement it, or speculate about its implementation
# """
#class ArrayReader:
#    def get(self, index: int) -> int:

class Solution:
    def search(self, reader: 'ArrayReader', target: int) -> int:
        # Corner Case
        if reader.get(0) == target:
            return 0

        left = 0
        right = 1

        # if reader.get(right) !< target, meaning target must exists in the [left, right]
        while reader.get(right) < target:
            left = right
            right *= 2

        # Binary Search
        while left <= right:
            mid = left + (right - left) // 2
            if reader.get(mid) == target:
                return mid
            elif reader.get(mid) > target:
                right = mid - 1
            else:
                left = mid + 1

        return -1
```
