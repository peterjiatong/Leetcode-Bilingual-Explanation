# [134. Gas Station](https://leetcode.com/problems/gas-station/)

[中文版本](/Solution_CN/0134_Gas_Station_CN.md)

## Solution

To solve this question, let's set up two variables: `total` and `curr`. The `total` represents the total fuel left after the whole trip (no matter where we start, the value of `total` should be the same), and `curr` represents the current gas left from the closest valid starting gas station. And, if the following statements are true, we can find the answer with one pass,:

i) If `total` >= 0, then there must be at least one valid starting station.

ii) Since the answer is **guaranteed** to be  **unique** , if `total` >= 0, the earliest station with `curr` >= 0 is the answer.

iii) When `curr` < 0 (at index i), we can safely ignore all stations before it.

iv) If `total` < 0, then the answer does not exist, return -1.

This solution has an O(n) time complexity and O(1) space complexity (since only constant space is used).

Java:

```java
class Solution {
    public int canCompleteCircuit(int[] gas, int[] cost) {
        int total = 0; // Total fuel left after the whole trip
        int curr = 0; // Current gas left from the closest valid starting gas station
        int answer = 0;

        for (int i = 0; i < gas.length; i++) {
            total += (gas[i] - cost[i]);
            curr += (gas[i] - cost[i]);

            if (curr < 0) { // Statement iii
                answer = i + 1; //statement ii
                curr = 0;
            }
        }

        if (total >= 0) { // Statement i
            return answer;
        } else {
            return -1; // Statement iv
        }
    }
}

// Tong
```

Python:

```python
class Solution:
    def canCompleteCircuit(self, gas: List[int], cost: List[int]) -> int:
        total = 0 # Total fuel left after the whole trip
        curr = 0 # Current gas left from the closest valid starting gas station
        answer = 0

        for i in range(len(gas)):
            total += gas[i] - cost[i]
            curr += gas[i] - cost[i]

            if curr < 0: # Statement iii
                answer = i + 1 # Statement ii
                curr = 0
  
        if total >= 0:  # Statement i
            return answer
        else: # Statement iv
            return -1

# Tong
```
