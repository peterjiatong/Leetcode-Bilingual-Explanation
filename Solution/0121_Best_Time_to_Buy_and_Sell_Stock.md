# Best Time to Buy and Sell Stock / 买卖股票的最佳时机

Leetcode: https://leetcode.com/problems/best-time-to-buy-and-sell-stock/

中文力扣：https://leetcode.cn/problems/best-time-to-buy-and-sell-stock/

## Description / 题目描述

You are given an array `prices` where `prices[i]` is the price of a given stock on the `i<sup>th</sup>` day.

You want to maximize your profit by choosing a **single day** to buy one stock and choosing a **different day in the future** to sell that stock.

Return  *the maximum profit you can achieve from this transaction* . If you cannot achieve any profit, return `0`.

给定一个数组 `prices` ，它的第 `i` 个元素 `prices[i]` 表示一支给定股票第 `i` 天的价格。

你只能选择 **某一天** 买入这只股票，并选择在 **未来的某一个不同的日子** 卖出该股票。设计一个算法来计算你所能获取的最大利润。

返回你可以从这笔交易中获取的最大利润。如果你不能获取任何利润，返回 `0` 。


## Solution 1: Brute-force / 蛮力法

The first method is relatively simple, use 2 for-loops to iterate through the array `prices`. A variable `profit` is used to record the maximum profit. If the difference between the current two elements is greater than `profit`, then update `profit`. After completing the iteration, return `profit`.

This solution has a O(n^2) time complexity, Note that Leetcode will not accept this solution due to "Time Limit Exceeded"

第一种解法较为简单，使用两个for循环的嵌套遍历数组 `prices`，使用一个变量 `profit`来记录最大差值，若当前的两个元素的差值大于 `profit`，则更新 `profit`至当前差值，遍历完成后返回 `profit`的值

此解法时间复杂度为 `O(n^2)`，力扣会因为 "超过时间限制"而不接受此答案。


Java:

```java
class Solution {
    public int maxProfit(int[] prices) {
        // Corner-case check
        if(prices.length == 1) return 0;

        int profit = 0;
        for(int i = 0; i < prices.length - 1; i++){
            for(int j = i + 1; j < prices.length; j++){
                if(prices[j] > prices[i]){
                    int temp = prices[j] - prices[i];
                    if(temp > profit){
                        profit = temp;
                    }
                }
            }
        }
        return profit;
    }
}

```

python:

```python
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        # Corner-case check
        if len(prices) == 1:
            return 0

        profit = 0
        for i in range(len(prices) -  1):
            for j in range(i + 1, len(prices)):
                if prices[j] > prices[i]:
                    temp = prices[j] - prices[i]
                    if temp > profit:
                        profit = temp
  
        return profit

```



## Solution 2: One Pass Traverse / 一次遍历

This is similer to solution 1, however we only need to iterates the given array once, we can maintain 2 variables, min corresponding to the lowest price and profit corresponding to the maximum profit.

This approach has a O(n) time complexity.

此解法的解题思路与解法1类似，但我们只需遍历给定数组一次，使用两个变量记录即可，min 对应最低价格，profit 对应最高利润。

这种方法的时间复杂度为 O(n)。


Java:

```java
class Solution {
    public int maxProfit(int[] prices) {
        // Corner-case check
        if(prices.length == 1) return 0;
        int min = prices[0];
        int profit = 0;

        for(int i = 1; i < prices.length; i++){
            if (prices[i] < min){
                min = prices[i];
            }else if(profit < prices[i] - min){
                profit = prices[i] - min;
            }
        }
        return profit;
    }
}

```

Python:

```python
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        # Corner-case check
        if len(prices) == 1:
            return 0
        min = prices[0]
        profit = 0
        for i in range(1, len(prices)):
            if prices[i] < min:
                min = prices[i]
            elif profit < prices[i] - min:
                profit = prices[i] - min

        return profit

```
