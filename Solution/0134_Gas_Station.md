# Gas Station / 加油站

Leetcode: https://leetcode.com/problems/gas-station/

中文力扣：https://leetcode.cn/problems/gas-station/

## Description / 题目描述

There are `n` gas stations along a circular route, where the amount of gas at the `ith` station is `gas[i]`.

You have a car with an unlimited gas tank and it costs `cost[i]` of gas to travel from the `ith` station to its next `(i + 1)th` station. You begin the journey with an empty tank at one of the gas stations.

Given two integer arrays `gas` and `cost`, return *the starting gas station's index if you can travel around the circuit once in the clockwise direction, otherwise return* `-1`. If there exists a solution, it is **guaranteed** to be **unique**

在一条环路上有 `n` 个加油站，其中第 `i` 个加油站有汽油 `gas[i]` 升。

你有一辆油箱容量无限的的汽车，从第 `i` 个加油站开往第 `i+1` 个加油站需要消耗汽油 `cost[i]` 升。你从其中的一个加油站出发，开始时油箱为空。

给定两个整数数组 `gas` 和 `cost` ，如果你可以按顺序绕环路行驶一周，则返回出发时加油站的编号，否则返回 `-1` 。如果存在解，则 **保证** 它是 **唯一** 的。

## Solution: Math / 数学法

Create two variables: `total` and `curr`, to keep track of the total amount of fuel that can be obtained during the journey and the total fuel that can be obtained from the last possible starting gas station, respectively.

When the total amount of fuel `total` becomes negative after iterating all stations, it's impossible to have a valid solution.

According to the question, if a solution exists, it is **guaranteed** to be **unique.** So, the first possible solution that can be found based on `curr` when `total > 0` will be the valid one.

Iterate through all the gas stations, and when `curr` becomes negative, set the next gas station as the possible starting station and reset `curr`.

After iteration, if `total < 0`, return -1.

This solution only requires iterating through the array once, so the time complexity is O(n).

创建两个变量：`total` 和 `curr`，分别记录行驶中总共能获得的油量，和从最近的可能是出发站的加油站出发后可能获得的总油量。

当总共能获得的油量 `total`小于0时，不可能有有效解。

根据题目，如果存在解，则 **保证** 它是 **唯一** 的，所以通过 `curr`能找到的第一个可能的解在满足 `total`大于0时，就一定是有效解

遍历全部的加油站，当 `curr`小于0时，设定下一个加油站为可能解，重置 `curr`

结束遍历后，若 `total`小于0，则返回-1

此解法只需要遍历数组一次，故时间复杂度为 `O(n)`

Java:

```java
class Solution {
    public int canCompleteCircuit(int[] gas, int[] cost) {
        int total = 0;
        int curr = 0;
        int answer = 0;

        for (int i = 0; i < gas.length; i++) {
            total += (gas[i] - cost[i]);
            curr += (gas[i] - cost[i]);

            if (curr < 0) {
                answer = i + 1; // We can safely ignore station before i since curr < 0
                curr = 0;
            }
        }

        if (total >= 0) {
            return answer;
        } else {
            return -1;
        }
    }
}

```

Python:

```python
class Solution:
    def canCompleteCircuit(self, gas: List[int], cost: List[int]) -> int:
        total = 0
        curr = 0
        answer = 0

        for i in range(len(gas)):
            total += gas[i] - cost[i]
            curr += gas[i] - cost[i]

            if curr < 0:
                answer = i + 1 # We can safely ignore station before i since curr < 0
                curr = 0
  
        if total >= 0:
            return answer
        else:
            return -1

```
