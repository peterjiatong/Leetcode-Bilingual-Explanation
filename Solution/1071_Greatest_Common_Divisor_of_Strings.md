# 1071. Greatest Common Divisor of Strings / 字符串的最大公因子

Leetcode: https://leetcode.com/problems/greatest-common-divisor-of-strings/description/

力扣：https://leetcode.cn/problems/greatest-common-divisor-of-strings/description/

## Solution 1: Traverse / 遍历

We know that if two strings share a common divisor, then at least one prefix of the shorter string must also be a prefix of the longer string. So we first compare the lengths of the two strings and take the length of the shorter string. Then, we use a for loop to iterate from that length down to 1. The first common divisor we find during traverse will be the greatest common divisor.

我们知道如果两个字符串存在公因子，那较短的字符串至少存在一个前缀同时也是较长的字符串的前缀，所以先比较两个字符串的长度，取较短的字符串的长度，使用for循环从大到小遍历，第一个在遍历过程中找到的公因子就是最大的公因子

Java


Python

```python
class Solution:
    def gcdOfStrings(self, str1: str, str2: str) -> str:
        for i in range(min(len(str1), len(str2)), 0, -1):
            if len(str1) % i or len(str2) % i:
                continue

            prefix = str1[:i]
            mul1 = len(str1) // i
            mul2 = len(str2) // i

            if str1 == prefix * mul1 and str2 == prefix * mul2:
                return prefix

        return ""
```

## Solution 2: Length‘s GCD / 长度的最大公因数

If two strings share a common divisor, then `str1 + str2` must be equal to `str2 + str1`.

If this condition is met, we only need to find the GCD of the lengths of the two strings to figure out the answer.

This method not only uses mathematical thinking, but also significantly reduces the time complexity.

(Assuming `a` and `b` are the lengths of `str1` and `str2`, respectively: The first approach involves multiple comparisons, so its time complexity is `O(min(a, b) * (a + b))`, the second approach requires only a single comparison, so its time complexity is `O(a + b)`.)

如果两个字符串存在公因子，那么 `str1 + str2` 等于 `str2 + str1`

如果上述条件达成，我们只需要找到两个字符串的长度的最大公因数就可以找到答案了

此方法不仅在体现了数学思维，同时也大幅降低了时间复杂度（a,b 为字符串1，2的长度: 解法一需要对比多次，所以时间复杂度为 `O(min(a,b) * a+b`)， 而解法二只需要对比一次，所以时间复杂度为 `O(m+n)`)

Java


Python

```python
class Solution:
    def gcdOfStrings(self, str1: str, str2: str) -> str:
        if str1 + str2 != str2 + str1:
            return ""

        prefix_len = gcd(len(str1), len(str2))
        return str1[:prefix_len]
```
