# 509. Fibonacci Number / 斐波那契数

leetcode: https://leetcode.com/problems/fibonacci-number/description/

力扣： https://leetcode.cn/problems/fibonacci-number/description/

## Solution 1: Brute Force / 暴力法

Using a recursive approach results in a time complexity of `O(2^n)`, I do not recommend this solution.

使用递归方法，时间复杂度为 `O(2^n)`，我比较不推荐此解法

Java

```java
class Solution {
    public int fib(int n) {
        if (n == 0 || n == 1) return n;
    
        return fib(n - 1) + fib(n - 2);
    }
}
```

Python

```python
class Solution:
    def fib(self, n: int) -> int:
        if n == 0 or n == 1:
            return n
	# use self. to call the method itself
        return self.fib(n - 1) + self.fib(n - 2)
```

## Solution 2: Dynamic Programming / 动态规划

Using dynamic programming, we create an array of length `n` and update it so that the element at index `i` corresponds to the value of `fib(i)`. The final result `fib(n)` is the sum of the last and second-to-last elements in the array. This algorithm has a time complexity of `O(n)` and a space complexity of `O(n)`.

使用动态规划，创建一个长度为 `n`的数组，更新数组使得数组中的下标 `i`的元素对应 `fib(i)`的结果，最终fib(n)的结果就是数组中倒数第一个数和倒数第二个数之和，此算法时间复杂度为 `O(n)`，空间复杂度也为 `O(n)`

Java

```java
class Solution {
    public int fib(int n) {
        // Corner case
        if (n == 0 || n == 1) return n;
    
        // init field
        int[] res = new int[n];
        res[0] = 0;
        res[1] = 1;

        for (int i = 2; i < n; i++) {
            res[i] = res[i - 1] + res[i - 2];
        }

        return res[n - 1] + res[n - 2];
    }
}
```

Python

```python
class Solution:
    def fib(self, n: int) -> int:
        # Corner case
        if n == 0 or n == 1:
            return n
	# init
        res = [0] * n
        res[0] = 0
        res[1] = 1

	# fill in values for the dp array
        for i in range(2, n):
            res[i] = res[i-1] + res[i-2]

        return res[-1] + res[-2]
```

## Solution 3: Iterative / 迭代法

This method only needs to keep track of the previous two results and the current result. In each iteration, we update these values accordingly. The time complexity is `O(n)` and the space complexity is `O(1)`.	

此方法只需要记录前两个的结果和当前结果，每次迭代更新这些结果即可，时间复杂度为 `O(n)`，空间复杂度为 `O(1)`

Java

```java
class Solution {
    public int fib(int n) {
        // Corner case
        if (n == 0 || n == 1) return n;
    
        int prevprev = 0;
        int prev = 1;
        int cur = 1;

        for (int i = 2; i <= n; i++) {
            cur = prevprev + prev;
            prevprev = prev;
            prev = cur;
        }

        return cur;
    }
}
```

Python

```python
class Solution:
    def fib(self, n: int) -> int:
        # Corner case
        if n == 0 or n == 1:
            return n

        prevprev = 0
        prev = 1
        cur = 1

        for i in range(2, n + 1):
            cur = prevprev + prev
            prevprev = prev
            prev = cur

        return cur
```
