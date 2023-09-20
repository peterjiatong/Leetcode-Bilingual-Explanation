# [39. Combination Sum](https://leetcode.com/problems/combination-sum/)

[中文版本](/Solution_CN/0039_Combination_Sum_CN.md)

## Solution: Backtracking

The idea of backtracking is to find all valid combinations using recursion. Since this question requires us to find combinations that include the same numbers, we also need to track combinations containing identical numbers.

![exploration tree](https://leetcode.com/problems/combination-sum/Figures/39/39_exploration_tree.png)

The picture above (from LeetCode) demonstrates the concept well. If the sum of the current combination is less than the target, we can add another number to the combination. If the sum of the current combination is equal to the target, we can record that combination as valid. If the sum of the current combination exceeds the target, we can discard that path, as it is impossible to find a valid solution with the current combination.

Let n be the size of the given candidates, T be the target, and Min be the minimum value among the candidates. The maximum depth of the "tree" we build would be (T/Min) + 1. Therefore, this solution has a time complexity of O(n^((T/Min) + 1)).


Java

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

//Tong, 9/19/2023
```

Python

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

# Tong, 9/19/2023
```
