# Search a 2D Matrix / 搜索二维矩阵

Leetcode: https://leetcode.com/problems/search-a-2d-matrix/

中文力扣：https://leetcode.cn/problems/search-a-2d-matrix/

## Description / 题目描述

You are given an `m x n` integer matrix `matrix` with the following two properties:

* Each row is sorted in non-decreasing order.
* The first integer of each row is greater than the last integer of the previous row.

Given an integer `target`, return `true` *if* `target` *is in* `matrix` *or* `false`  *otherwise* .

You must write a solution in `O(log(m * n))` time complexity.

给你一个满足下述两条属性的 `m x n` 整数矩阵：

* 每行中的整数从左到右按非严格递增顺序排列。
* 每行的第一个整数大于前一行的最后一个整数。

给你一个整数 `target` ，如果 `target` 在矩阵中，返回 `true` ；否则，返回 `false` 。

## Solution: Binary Search / 二分搜索

This problem uses a standard binary search approach. The key is to convert a one-dimensional index into a two-dimensional index to perform the search.

After we get value of  `mid`, we convert it into `[mid / matrix[0].length][mid % matrix[0].length]` before performing the binary search.

This algorithm has a time complexity of `O(log (m*n))`, where `m` is the number of rows and `n` is the number of columns.

本题采用标准的二分搜索，只需要将一维的下标转换为二维的下标再做搜索即可:

每次计算出`mid`的值后，将其转换为 `[mid / matrix[0].length][mid % matrix[0].length]`后在进行二分搜索即可

此算法时间复杂度为 `O(log (m*n))`，`m`为行数，`n`为列数。

Java

```java
class Solution {
    public boolean searchMatrix(int[][] matrix, int target) {
        int rows = matrix.length;
        int cols = matrix[0].length;
        int left = 0;
        int right = rows * cols - 1;

        while(left <= right){
            int mid = left + (right - left) / 2;
            int curRow = mid / cols;
            int curCol = mid % cols;

            if (matrix[curRow][curCol] == target) return true;
            else if (matrix[curRow][curCol] > target) right = mid - 1;
            else left = mid + 1;
        }

        return false;
    }
}

```

Python

```python
class Solution:
    def searchMatrix(self, matrix: List[List[int]], target: int) -> bool:
        rows = len(matrix)
        cols = len(matrix[0])
        left = 0
        right = rows * cols - 1

        while (left <= right):
            mid = (left + right) // 2
            curRow = mid // cols
            curCol = mid % cols
      
            if matrix[curRow][curCol] == target:
                return True
            elif matrix[curRow][curCol] > target:
                right = mid - 1
            else:
                left = mid + 1
   
        return False
```
