# [217. 存在重复元素](https://leetcode.com/problems/contains-duplicate/)

[English Ver.](/Solution/0217_Contains_Duplicate.md)

## 解法：哈希集

哈希集是这类问题的最佳数据结构选择之一，因为它对于搜索和插入只需 `O(1)` 的时间复杂度。我们可以遍历给定数组 `nums`。如果 `nums[i]`在哈希集中，就返回 `true`；否则，将 `nums[i] `添加到哈希集中。

此解法的时间复杂度和空间复杂度均为`O(n)`，因为我们使用了一个哈希集

Java解法

```java
class Solution {
    public boolean containsDuplicate(int[] nums) {
	// Use HashSet because it take O(1) for both search and insert
        HashSet<Integer> seen = new HashSet<>();
        for (int num: nums){
            if (seen.contains(num)){
                return true;
            }
            seen.add(num);
        }

        return false;
    }
}

// Tong, 9/22/2023
```

Python解法

```python
class Solution:
    def containsDuplicate(self, nums: List[int]) -> bool:
        # set in python functions the same as hashset
        seen = set()
        for num in nums:
            if num in seen:
                return True
            seen.add(num)
        return False

# Tong, 9/22/2023
```
