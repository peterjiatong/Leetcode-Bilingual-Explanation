# [Two Sum](https://leetcode.com/problems/two-sum/)

[英文版本](/Solution/0001_Two_Sum.md)

## 题解

**解法1: 蛮力法**

本题最简单的解法是使用2个for循环，外循环从第一个元素遍历到倒数第二个元素（记为 i），内循环从i遍历到最后一个元素， 每次检查每两个元素之和是等于target。

本解法的时间复杂度为O(n^2)。

### Java

```java

classSolution {

publicint[] twoSum(int[] nums, inttarget) {

// Iterates from index 0 to nums.length - 1

for (inti = 0; i < nums.length - 1; i++) {

// Iterates from i to nums.length

for (intj = i + 1; j < nums.length; j++) {

// If their sum equals to target, return {i, j}

if (nums[i] + nums[j] == target) {

returnnewint[]{i, j};

                }

            }

        }

// In case no solution found

returnnewint[]{};

    }

}

```

### Python

```python

classSolution:

deftwoSum(self, nums: List[int], target: int) -> List[int]:

# Iterates from index 0 to nums.length - 1

for i inrange(len(nums) - 1):

# Iterates from i to nums.length

for j inrange(i + 1, len(nums)):

# If their sum equals to target, return {i, j}

if nums[i] + nums[j] == target:

return [i, j]

```

**解法2: 哈希表**

此解法将（target - num[i]，index i）存储到哈希表中。当我们遍历数组 nums 时，如果在哈希表中找到 nums[i]，就说明我们找到了题解。

因为哈希表可以在 O（1） 时间内搜索，因此此解决方案的时间复杂度为 O（n）。

### Java

```java

classSolution {

publicint[] twoSum(int[] nums, inttarget) {

// Creates a hash map the takes an integer as key and an integer as value

HashMap<Integer,Integer> values = newHashMap<>();

// Iterates the given array nums

for (inti = 0; i < nums.length; i++){

// If we found nums[i] in the hashmap, return

if(values.containsKey(nums[i])){

returnnewint[] {i, values.get(nums[i])};

            }

// Else, put target - nums[i] and its index in the hashmap

values.put(target - nums[i], i);

        }

// In case no solution found

returnnewint[]{};

    }

}

```

### Python

```python

classSolution:

deftwoSum(self, nums: List[int], target: int) -> List[int]:

# because dict() in python in based on hashmap, we don't have to pecifically set up a hashmap

        values = dict()

# Iterates the given array nums

for i inrange(0, len(nums)):

# If we found nums[i] in the hashmap, return

if nums[i] in values:

return (i, values[nums[i]])

# Else, put target - nums[i] and its index in the hashmap

            values[target - nums[i]] = i

```

### C++

```c++

classSolution {

public:

vector<int> twoSum(vector<int>&nums, inttarget) {

        // Create a map of values w/ indices of the elements "looking for it"

        unordered_map<int, int> map;


        // For each number in nums

for (int i = 0; i < nums.size(); i++) {

            // If the element is in the map, return the indices

auto it = map.find(nums[i]);

if (it != map.end()) return {it->second, i};


            // Else store target - current element with the current index

map[target - nums[i]] = i;

        }


return {}; // Solution not found, return empty vector. SHOULD NOT HAPPEN!

    }

};

```
