# Sliding Window Maximum /  滑动窗口最大值

Leetcode: https://leetcode.com/problems/sliding-window-maximum/

中文力扣：https://leetcode.cn/problems/sliding-window-maximum/

## Description / 题目描述

You are given an array of integers `nums`, there is a sliding window of size `k` which is moving from the very left of the array to the very right. You can only see the `k` numbers in the window. Each time the sliding window moves right by one position.

Return  *the max sliding window* .

给你一个整数数组 `nums`，有一个大小为 `k` 的滑动窗口从数组的最左侧移动到数组的最右侧。你只可以看到在滑动窗口内的 `k` 个数字。滑动窗口每次只向右移动一位。

返回  *滑动窗口中的最大值* 。

## Solution: Deque / 双端队列

Create a double-ended queue to keep track of the indices of valid elements within the current index window. For any given element `nums[i]` in the array, it will only affect the window `[i - k + 1, i + k -1]`. Since the goal is to find the maximum value within the window, it is sufficient to record the indices of the maximum value and larger values after it within the window `[i - k + 1, i + k -1]`. Recording indices instead of element values allows for better determination of whether the largest element in the deque is still within the valid window. Traverse the given array `nums`:

1. If there are elements in the `deque` and the first element is out of bounds (i.e., it's no longer within the current window), remove it from the `deque`.
2. If there are elements in the `deque`, start from the tail of the deque and check each element. Remove all elements that are less than or equal to the current `nums[i]`.
3. Add the current `nums[i] `to the `deque`.
4. Record the first element of the deque as the maximum value for the current window.

Each element in the array is added to the deque only once and can also be removed only once, so the time complexity of this algorithm is `O(n)`.

创建一个双端队列用于记录当前下标窗口中的有效元素的下标，对于给定数组中的任意元素nums[i], 只会作用在`[i - k + 1, i + k -1]`的窗口中，又因为我们需要寻找窗口中，所以对于`nums[i]`而言，我们只需记录`[i - k + 1, i + k -1]`的窗口中最大值和在其之后较大的值即可。记录下标而不是元素的值可以让我们更好的判断双端队列中最大的元素是否还处于有效的窗口中。遍历给定数组`nums`：

1. 若当前双端队列中有元素，且第一个元素出界，则将其移除双端队列
2. 若当前双端队列中有元素，从队尾开始检查队列中的元素，移除所有小于等于当前`nums[i]`的元素
3. 将当前`nums[i]`加入双端队列中
4. 记录双端队列的第一个元素为当前窗口的最大值

每个元素只会被添加至双端队列一次，同时也只能被移除一次，所以此算法时间复杂度为`O(n)`

Java

```java
class Solution {
    public int[] maxSlidingWindow(int[] nums, int k) {
        Deque<Integer> curWindow = new ArrayDeque<>();
        List<Integer>  ans = new ArrayList<>();

        for (int i = 0; i < k; i++){
            while (!curWindow.isEmpty() && nums[i] >= nums[curWindow.peekLast()]){
                curWindow.pollLast();
            }
            curWindow.offerLast(i);
        }

	// Append the first answer after done scanning all elements of the first window
        ans.add(nums[curWindow.peekFirst()]);
  
        for(int i = k; i < nums.length; i++){
            if (!curWindow.isEmpty() && curWindow.peekFirst() == i - k){
                curWindow.pollFirst();
            }
            while (!curWindow.isEmpty() && nums[i] >= nums[curWindow.peekLast()]){
                curWindow.pollLast();
            }
            curWindow.offerLast(i);
            ans.add(nums[curWindow.peekFirst()]);  
        }

      	// Modify the output type
	int[] result = new int[ans.size()];
        for (int i = 0; i < ans.size(); i++){
            result[i] = ans.get(i);
        }

        return result;
    }
}
```

Python

```python
class Solution:
    def maxSlidingWindow(self, nums: List[int], k: int) -> List[int]:
        curWindow = deque()
        ans = []

        for i in range(k):
            while len(curWindow) > 0 and nums[i] >= nums[curWindow[-1]]:
                curWindow.pop()
            curWindow.append(i)
  
	# Append the first answer after done scanning all elements of the first window
        ans.append(nums[curWindow[0]])

        for i in range(k, len(nums)):
            if len(curWindow) > 0 and curWindow[0] == i - k:
                curWindow.popleft()
            while len(curWindow) > 0 and nums[i] >= nums[curWindow[-1]]:
                curWindow.pop()
  
            curWindow.append(i)
            ans.append(nums[curWindow[0]])
  
        return ans

```
