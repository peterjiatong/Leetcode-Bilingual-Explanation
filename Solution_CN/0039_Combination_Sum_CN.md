# [39。组合总和](https://leetcode.com/problems/combination-sum/)

[English Ver.](/Solution/0039_Combination_Sum.md)

## 解法：回溯法

回溯法的思路是通过递归来找出所有有效的组合。因为这个问题要求我们找到包含相同数字的组合，我们也需要追踪包含相同数字的组合。

![exploration tree](https://leetcode.com/problems/combination-sum/Figures/39/39_exploration_tree.png)

上面的图片（来源： LeetCode）很好地展示了这个解法的思路。如果当前组合的和小于目标值，我们可以向组合中添加另一个数字以找到新的组合。如果当前组合的和等于目标值，我们记录下当前组合。如果当前组合的和超过目标值，我们可以舍弃当前路径，因为用当前组合不可能找到一个有效的解决方案。

设 n 为给定候选数组的大小，T 为目标值，Min 为候选数组中的最小值。我们构建的“树”的最大深度将是 (T/Min) + 1。因此，这个解决方案的时间复杂度为 O(n^((T/Min) + 1))。

Java:

```java
class Solution {
    private void backtrack(int target, int index, int[] candidates, List<List<Integer>> ans, List<Integer> path){
        // This target = given target - sum of path, therefore, if this target == 0, current path is a vaild answer
        if (target == 0){
            ans.add(new ArrayList<Integer>(path));
            return;
        // This target < 0 means sum of current path is greater than the actual target
        }else if (target < 0) return;

         for (int i = index; i < candidates.length; ++i) {
            path.add(candidates[i]); // Find all combinations
            // Call function itself allows us to track same numbers
            backtrack(target - candidates[i], i, candidates, ans, path); 
            // if we reach base case, wall breaks, we remove the last index of path in order to get another possible vaild combinations
            path.remove(path.size() - 1);
         }
    }

    public List<List<Integer>> combinationSum(int[] candidates, int target) {
        List<List<Integer>> ans = new ArrayList<List<Integer>>();
        // Keep track all the combinations
        List<Integer> path = new ArrayList<Integer>();

        backtrack(target, 0, candidates, ans, path);
        return ans;
    }
}

// Tong
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
            # This target < 0 means sum of current path is greater than the actual target
            elif target < 0:
                return
  
            for i in range(index, len(candidates)):
                path.append(candidates[i]) # Find all combinations
                backtrack(target - candidates[i], i, path)
                # if we reach base case, wall breaks, we remove the last index of path in order to get another possible vaild combinations
                path.pop()

        backtrack(target, 0, [])

        return ans

# Tong
```
