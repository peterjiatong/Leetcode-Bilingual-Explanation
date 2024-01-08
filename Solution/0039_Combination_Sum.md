# Combination Sum / 组合总和

Leetcode: https://leetcode.com/problems/combination-sum/

中文力扣：https://leetcode.cn/problems/combination-sum/

## Description / 题目描述

Given an array of **distinct** integers `candidates` and a target integer `target`, return *a list of all **unique combinations** of *`candidates`* where the chosen numbers sum to *`target`*.* You may return the combinations in  **any order** .

The **same** number may be chosen from `candidates` an  **unlimited number of times** . Two combinations are unique if the

frequency

 of at least one of the chosen numbers is different.

The test cases are generated such that the number of unique combinations that sum up to `target` is less than `150` combinations for the given input.

给你一个 **无重复元素** 的整数数组 `candidates` 和一个目标整数 `target` ，找出 `candidates` 中可以使数字和为目标数 `target` 的 所有 **不同组合** ，并以列表形式返回。你可以按 **任意顺序** 返回这些组合。

`candidates` 中的 **同一个** 数字可以 **无限制重复被选取** 。如果至少一个数字的被选数量不同，则两种组合是不同的。

对于给定的输入，保证和为 `target` 的不同组合数少于 `150` 个。

## Solution: Backtracking / 回溯法

This problem requires finding all possible combinations where the same number can be repeatedly chosen. We can use the backtracking to solve this question. The core of backtracking is to recursively explore all possible combinations, working from back to the front until all solutions are found.

First, Let's define two variables: `ans` to keep track all valid combinations, and `path` to record the current exploration path.

Starting from the first element of the given `candidates` array, we recursively try each possible combination. At each step, we add the current number to `path` and check the total sum of the numbers in `path`. If this sum equals to the `target`, then the current `path` is a valid combination, and we add it to `ans`. If the sum is less than `target`, we continue the recursion, adding the next possible number to `path`. If the sum exceeds `target`, we no longer need to continue with the current path.

After exploring each branch, we backtrack to the previous decision point and remove the last element in `path`, continuing until all possible combinations are explored.

The time complexity of this algorithm is `O(n^t)`, where `t` is the number of levels in the tree, generally equals to `(target/smallest element) + 1`.

本题目要求找出所有可能的组合，其中同一个数字可以无限次重复选取。为了解决这个问题，我们使用回溯法。回溯法的核心是通过递归探索所有可能的组合，从后向前直到找到所有符合条件的解。

首先定义两个变量：`ans`用于记录所有有效的组合，`path`用于记录当前探索的路径。

从给定的 `candidates`数组的第一个元素开始，递归地尝试每一个可能的组合。在每一步中，我们将当前的数字添加到 `path`中，并检查 `path`中数字的总和。如果这个总和等于目标 `target`，则当前 `path`是一个有效的组合，我们将其添加到 `ans`中。如果总和小于 `target`，我们继续递归，添加下一个可能的数。如果总和超过 `target`，则不再进一步探索当前路径。

每当探索完一个分支后，我们回溯到上一个决策点，并移除 `path`中的最后一个元素，直到探索完所有可能的组合。

此算法时间复杂度为 `O(n^t)`，其中 `t`为树的层数，一般情况下为 `(target/最小元素) + 1`

![exploration tree](https://leetcode.com/problems/combination-sum/Figures/39/39_exploration_tree.png)

(picture above from leetcode solutions)



Java:

```java
class Solution {
    private void backtrack(int target, int index, int[] candidates, List<List<Integer>> ans, List<Integer> path){
        // This target = given target - sum of path, therefore, if this target == 0, current path is a vaild answer
        if (target == 0){
            ans.add(new ArrayList<Integer>(path));
            return;
        }else if (target < 0) return;

         for (int i = index; i < candidates.length; ++i) {
            path.add(candidates[i]);
            backtrack(target - candidates[i], i, candidates, ans, path); 
            path.remove(path.size() - 1);
         }
    }

    public List<List<Integer>> combinationSum(int[] candidates, int target) {
        List<List<Integer>> ans = new ArrayList<List<Integer>>();
        List<Integer> path = new ArrayList<Integer>();
        backtrack(target, 0, candidates, ans, path);
        return ans;
    }
}

```

Python:

```python
class Solution:
    def combinationSum(self, candidates: List[int], target: int) -> List[List[int]]:
        ans = []

        # This target = given target - sum of path, therefore, if this target == 0, current path is a vaild answer
        def backtrack(target, index, path):

            if target == 0:
		# Make sure we make a copy of path here, so later changes will not affect the ans. 
                ans.append(copy.copy(path))
                return
            elif target < 0:
                return
  
            for i in range(index, len(candidates)):
                path.append(candidates[i])
                backtrack(target - candidates[i], i, path)
                path.pop()

        backtrack(target, 0, [])
        return ans

```
