# [278. 第一个错误的版本](https://leetcode.com/problems/first-bad-version/)

[English Ver.](/Solution/0278_First_Bad_Version.md)

## 解法：二分搜索

我们可以通过使用二分搜索来找到第一个错误的版本。使用此方法中可能出现的两种情况：

1. 如果 `mid` 是错误的版本，我们更新 `right = mid`。
2. 如果 `mid` 不是错误的版本，我们更新 `left = mid + 1`。因为我们要找到第一个错误的版本，所以我们可以忽略非错误版本。

当 `left` 不小于 `right` 时我们停止；此时，`left` 应该指向我们的答案。

由于使用了二分搜索，这个解决方案的时间复杂度为`O(log n)`。

Java解法

```java
/* The isBadVersion API is defined in the parent class VersionControl.
      boolean isBadVersion(int version); */

public class Solution extends VersionControl {
    public int firstBadVersion(int n) {
        int left = 0;
        int right = n;
        while (left < right) {
            int mid = left + (right - left) / 2; // Prevent integer out of bound
            if (isBadVersion(mid)) {
                right = mid;
            } else {
                left = mid + 1; // If mid is a good version, skip it
            }
        }
        return left;
}
}

// Tong, 9/21/2023
```

Python解法

```python
# The isBadVersion API is already defined for you.
# def isBadVersion(version: int) -> bool:

class Solution:
    def firstBadVersion(self, n: int) -> int:
        left = 0
        right = n
        while left < right:
            mid = int ((left + right) / 2) # Python does not have an integer limit, however we need to regulate data type for mid in order to return an int
            if isBadVersion(mid):
                right = mid
            else:
                left = mid + 1 # If mid is a good version, skip it
  
        return left

# Tong, 9/21/2023
```
