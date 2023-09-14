# [买卖股票的最佳时机](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/)

## 解法1: 蛮力法
我们只需要在遍历给定数组时找到最大利润即可，可以使用2个for循环，其中外循环遍历从第一个元素到倒数第二个元素（记为i），内循环遍历从 i 到最后一个元素（记为j），结果为prices[i] - prices[j]之间的最大差值。

请注意，此解法的时间复杂度为 O(n^2)，力扣会因为 "超过时间限制"而不接受此答案。

### Java
```java
class Solution {
    public int maxProfit(int[] prices) {
        // Corner-case check
        if(prices.length == 1) return 0;

        int profit = 0;
        // Iterates from index 0 to nums.length - 1
        for(int i = 0; i < prices.length - 1; i++){
            // Iterates from i to nums.length
            for(int j = i + 1; j < prices.length; j++){
                // Check if this is a profit
                if(prices[j] > prices[i]){
                    int temp = prices[j] - prices[i];
                    // Check if current profit is greater than the profit we have
                    if(temp > profit){
                        profit = temp;
                    }
                }
            }
        }
        // Return profit, note that if there's no profit to make, we return 0
        return profit;
    }
}
```

### Python
```python
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        # Corner-case check
        if len(prices) == 1:
            return 0

        profit = 0
        # Iterates from index 0 to nums.length - 1
        for i in range(len(prices) -  1):
            # Iterates from i to nums.length
            for j in range(i + 1, len(prices)):
                # Check if this is a profit
                if prices[j] > prices[i]:
                    temp = prices[j] - prices[i]
                    # Check if current profit is greater than the profit we have
                    if temp > profit:
                        profit = temp
        
        # Return profit, note that if there's no profit to make, we return 0
        return profit
```

## 解法2：一次遍历
此解法的解题思路与解法1类似，但我们只需遍历给定数组一次，使用两个变量记录即可，min 对应最低价格，profit 对应最高利润。

这种方法的时间复杂度为 O(n)。

### Java
```java
class Solution {
    public int maxProfit(int[] prices) {
        // Corner-case check
        if(prices.length == 1) return 0;
        // Keep track of lowest price
        int min = prices[0];
        int profit = 0;

        // Iterates from index 1 because we already set min = prices[0]
        for(int i = 1; i < prices.length; i++){
            // Update min if we found a lower price
            if (prices[i] < min){
                min = prices[i];
            // Update profit if current profit is greater than the profit we have
            }else if(profit < prices[i] - min){
                profit = prices[i] - min;
            }
        }
        // Return profit, note that if there's no profit to make, we return 0
        return profit;
    }
}
```

### Python
```python
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        # Corner-case check
        if len(prices) == 1:
            return 0
        # Keep track of lowest price 
        min = prices[0]
        profit = 0
        # Iterates from index 1 because we already set min = prices[0]
        for i in range(1, len(prices)):
            # Update min if we found a lower price
            if prices[i] < min:
                min = prices[i]
            # Update profit if current profit is greater than the profit we have
            elif profit < prices[i] - min:
                profit = prices[i] - min
        
        # Return profit, note that if there's no profit to make, we return 0
        return profit
```
