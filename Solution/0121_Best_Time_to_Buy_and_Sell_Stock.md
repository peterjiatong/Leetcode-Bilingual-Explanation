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