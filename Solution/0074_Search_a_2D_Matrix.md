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

## Constraints **/ 提示**

* `m == matrix.length`
* `n == matrix[i].length`
* `1 <= m, n <= 100`
* `-10^4 <= matrix[i][j], target <= 10^4`

## Solution: Binary Search / 二分搜索

This problem utilizes standard binary search. It simply involves converting two-dimensional coordinates into one-dimensional indices for searching within the matrix `matrix`. The method to find the value corresponding to an integer index `index` in the matrix is given by `matrix[index / matrix[0].length][index % matrix[0].length]`.

The time complexity of this algorithm is `O(log (m*n))`, where `m` is the number of rows and `n` is the number of columns in the matrix.

本题采用标准的二分搜索，只需要将二维的坐标转换为一维之后，再进行搜索即可(在矩阵 `matrix`中使用整数下标 `index`找到其对应的值的方法为 `matrix[index / matrix[0].length][index % matrix[0].length]`)

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

## Solution: Binary Search Twice / 两次二分搜索

We can also first use binary search to determine which row the target is in, and then perform another binary search within that specific row.

This approach has a time complexity of `O(log m + log n)`.

我们也可以先使用二分搜索确定答案在那一行，然后再在对应的那一行中再进行一次二分搜索

此解法时间复杂度为 `O(log m + log n)`

Java

```java
class Solution {
    public boolean searchMatrix(int[][] matrix, int target) {
        int exact_line = find_line(matrix, target);
	//corner case
        if (exact_line == -1) return false;
  
	// binary search in specific row
	int left = 0;
        int right = matrix[0].length - 1;

        while (left <= right) {
            int mid = left + (right - left) / 2;
            int val = matrix[exact_line][mid];

            if (val == target) return true;
            else if (val < target) left = mid + 1;
            else right = mid - 1;
  
        }
        return false;

    }

    public int find_line (int[][] matrix, int target){
        // field
        int top = 0;
        int bot = matrix.length - 1;

        while (top <= bot){
            int mid = top + (bot - top) / 2;

            if (matrix[mid][0] > target) bot = mid - 1; 
            //means target exist above the mid line
            else if (matrix[mid][matrix[0].length - 1] < target) top = mid + 1;
            //means target exist below the mid line
            else return mid;
            // if matrix[mid][0] < target < matrix[mid][matrix[0], then return this mid
        }
  
        return -1; // if target doesn't exist in any line, then return -1
    }
}
```

Python

```python
class Solution:
    def searchMatrix(self, matrix: List[List[int]], target: int) -> bool:

        def find_exact_row(matrix, target):
            top = 0
            bottom = len(matrix) - 1

            while top <= bottom:
                mid = top + (bottom - top) // 2
                if matrix[mid][0] > target:
                    bottom = mid - 1
                elif matrix[mid][len(matrix[0]) - 1] < target:
                    top = mid + 1
                else:
                    return mid

            return -1

        exact_row = find_exact_row(matrix, target)

        if exact_row == -1:
            return False

        left = 0
        right = len(matrix[0]) - 1
        while left <= right:
            mid = left + (right - left) // 2
            if matrix[exact_row][mid] == target:
                return True
            elif matrix[exact_row][mid] > target:
                right = mid - 1
            else:
                left = mid + 1

        return False


```
