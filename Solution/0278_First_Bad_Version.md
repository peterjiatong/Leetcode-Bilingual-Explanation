# [278. First Bad Version](https://leetcode.com/problems/first-bad-version/)

[中文版本](/Solution_CN/0278_First_Bad_Version_CN.md)

## Solution: Binary Search

We can identify the first bad version using binary search. Below are two cases that may occur during the approach:

1. If `mid` is a bad version, we update `right = mid`.
2. If `mid` is a good version, we update `left = mid + 1`. This is because we are trying to find the first bad version, so we can safely ignore the good versions.

We stop when `left` is not less than `right`; at this point, `left` should point to our answer.

This solution has a time complexity of `O(log n)` due to the use of binary search.

Java:

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

// Tong
```

Python:

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

# Tong
```
