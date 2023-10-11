# [134. 加油站](https://leetcode.com/problems/gas-station/)

[English Ver.](/Solution/0134_Gas_Station.md)

解法

要解决这个问题，我们设定两个变量：`total` 和 `curr`。`total` 代表整个遍历整个数组后剩下的总燃料（无论我们从数组的哪里开始，`total` 的值都应该是相同的），而 `curr` 代表从最近的有效起始加油站剩下的当前油量。我们可以只遍历一次就找到答案，如果以下条件均为真：

i) 如果 `total` >= 0，那么至少有一个有效的起始加油站。

ii) 根据题目，由于答案是**唯一的** ，如果 `total` >= 0，那么最靠前的 `curr` >= 0 的加油站就是答案。

iii) 当 `curr` < 0（在索引 i 时），我们可以安全地忽略它( i )之前的所有加油站。

iv) 如果 `total` < 0，那么答案不存在，返回 -1。

这个解决方案的时间复杂度是 O(n) ，空间复杂度是 O(1)（因为只使用了固定空间）。

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
