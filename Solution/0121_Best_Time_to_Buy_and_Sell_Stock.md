<<<<<<< HEAD
# [Best Time to Buy and Sell Stock](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/)

## Solution 1: Brute-force
For this approach, we only need to find the max profit while iterates through the given array prices, we can use 2 for-loops, where the outer loop iterates from the first element to the second last element(notes as i), and the inner loop iterates from i to the last element(notes as j), return the max difference between prices[i] - prices[j]

Note that this solution has a O(n^2) time complexity, Leetcode will not accept this solution due to "Time Limit Exceeded"

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

## Solution 2: One Pass Traverse
This is similer to solution 1, however we only need to iterates the given array once, we can maintain 2 variables, min corresponding to the lowest price and profit corresponding to the maximum profit.

This approach has a O(n) time complexity.

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
=======
```python
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        # Initialize the maximum profit and the minimum price
        profit = 0
        minPrice = prices[0]
        
        # Iterate through the prices to calculate the maximum profit
        for price in prices:
            # Update the minimum price if the current price is lower
            if price < minPrice:
                minPrice = price
            else:
                # Calculate the potential profit and update the maximum profit
                profit = max(profit, price - minPrice)
        
        # Return the final maximum profit
        return profit
```
>>>>>>> f917540d67411d27320e8b972f35e5d8a655aede
