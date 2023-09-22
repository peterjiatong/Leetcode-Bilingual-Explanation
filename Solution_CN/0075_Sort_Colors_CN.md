# [75. 颜色分类]()

[English Ver.](/Solution/0075_Sort_Colors.md)

## 解法1：计数法 + 两次遍历

遍历给定的数组，以计算 0，1 和 2 的出现次数，并将这些计数存储在一个名为 `bucket`的变量中中，其中索引代表数字，值代表出现次数，类似于dict。然后，再次遍历以根据bucket中的值按顺序修改 'nums'。

此解决方案的时间复杂度为 `O(n)`，空间复杂度为 `O(3)`。

Java解法

```java
class Solution {
    public void sortColors(int[] nums) {
        int[] bucket = {0,0,0};

        for (int num : nums){
            bucket[num] ++;
        }

	// Count represent the current number, cumulative represent the current index
        int count = 0;
        int cumulative = 0;

        for (int value : bucket){
            for (int i = 0; i < value; i++){
                nums[cumulative] = count;
                cumulative ++;
            }
            count ++;
        }
    }
}

// Tong, 9/21/2023
```

Python 解法

```python
class Solution:
    def sortColors(self, nums: List[int]) -> None:
        """
        Do not return anything, modify nums in-place instead.
        """
        bucket = [0,0,0]

        for num in nums:
            bucket[num] += 1

      	# Count represent the current number, cumulative represent the current index
	count = 0
        cumulative = 0

        for num in bucket:
            for _ in range(num):
                nums[cumulative] = count
                cumulative += 1
            count += 1

# Tong, 9/21/2023
```

## 解决方案2：双指针 + 一次遍历

这个解决方案的思路是只遍历一次数组。如果当前索引处的值 == 0，就将其与左指针处的值交换。如果当前索引处的值 == 2，就将其与右指针处的值交换。如果当前索引处的值 == 1，我们忽略它。每次交换后需更新指针。

由于我们只遍历了一次数组，所以这个解决方案的时间复杂度为 `O(n)`，比解决方案1显著快。空间复杂度为 `O(1)`，因为交换只使用了固定的空间。

Java解法

```java
class Solution {
    public void sortColors(int[] nums) {
        int left = 0;
        int right = nums.length - 1;
        int curr = 0;

        while(curr <= right){
            if (nums[curr] == 0){ // Make sure every element get checked
                swap(nums, curr, left);
		// Update both curr and left because we already know that from index 0 to left are all 0s
                curr ++;
                left ++;
            }else if (nums[curr] == 2){
                swap(nums, curr, right);
		// Only update right because we can't make sure what happens on the left part
                right --;
            }else {
                curr ++;
            }
        }
}

// Tong, 9/21/2023
    public void swap(int[] nums, int p1, int p2){
        int temp = nums[p1];
        nums[p1] = nums[p2];
        nums[p2] = temp;
    }
}
```

Python解法

```python
class Solution:
    def sortColors(self, nums: List[int]) -> None:
        """
        Do not return anything, modify nums in-place instead.
        """
        left = 0
        right = len(nums) - 1
        curr = 0

        def swap(nums: List[int], p1: int, p2: int):
            temp = nums[p1]
            nums[p1] = nums[p2]
            nums[p2] = temp

        while(curr <= right): # Make sure every element got checked
            if nums[curr] == 0:
                swap(nums, curr, left)
		# Update both curr and left because we already know that from index 0 to left are all 0s
                curr += 1
                left += 1
            elif nums[curr] == 2:
                swap(nums, curr, right)
		# Only update right because we can't make sure what happens on the left part
                right -= 1
            else:
                curr += 1

# Tong, 9/21/2023
```
