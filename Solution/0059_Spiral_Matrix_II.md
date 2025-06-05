# 59. Spiral Matrix II / 螺旋矩阵 II

leetcode: https://leetcode.com/problems/spiral-matrix-ii/description/

力扣：https://leetcode.cn/problems/spiral-matrix-ii/description/

## Solution: Simulation / 模拟法

我认为本题难度不大，解题的关键在于要想清楚填入数组的顺序和后续如何更新边界，我的代码只是一种思路，仅供参考

Java

```java
class Solution {
    public int[][] generateMatrix(int n) {
        // Corner case
        if (n == 1) return new int [][] {{1}};
 
        int to_fill = 1;
        int[][] ans = new int[n][n];
        int left = 0;
        int right = n - 1;
        int top = 0;
        int bottom = n - 1;

        while (to_fill <= n*n) {
	    # fill-in the top layer
            for (int i = left; i <= right; i++) {
                ans[top][i] = to_fill;
                to_fill ++;
            }
            top ++;
	  
	    # fill-in the right side
            for (int i = top; i <= bottom; i++) {
                ans[i][right] = to_fill;
                to_fill ++;
            }
            right --;

	    # fill-in the bottom layer
            for (int i = right; i >= left; i--) {
                ans[bottom][i] = to_fill;
                to_fill ++;
            }
            bottom --;

	    # fill-in the left side
            for (int i = bottom; i >= top; i--) {
                ans[i][left] = to_fill;
                to_fill ++;
            }
            left ++;
        }


        return ans;
    }
}
```

Python

```python
class Solution:
    def generateMatrix(self, n: int) -> List[List[int]]:
        left = high = 0
        right = low = n - 1
        res = [[0] * n for _ in range(n)]
        count = 1

        while count < n * n:
            # fill-in the top layer
            for i in range(left, right + 1):
                res[high][i] = count
                count += 1
            high += 1

            # fill-in the right side
            for i in range(high, low + 1):
                res[i][right] = count
                count += 1
            right -= 1

            # fill-in the bottom layer
            for i in range(right, left - 1, -1):
                res[low][i] = count
                count += 1
            low -= 1

            # fill-in the left side
            for i in range(low, high - 1, -1):
                res[i][left] = count
                count += 1
            left += 1
        # post process for odd number n
        if n % 2 == 1:
            res[n // 2][n // 2] = count

        return res

```
