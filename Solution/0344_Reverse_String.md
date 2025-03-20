# Reverse String / 反转字符串

Leetcode: https://leetcode.com/problems/reverse-string/description/

中文力扣：https://leetcode.cn/problems/reverse-string/description/

## Solution: Two Pointers / 双指针

本题相对简单，做法偏多，这里只提供双指针的解法

Java

```java
class Solution {
    public void reverseString(char[] s) {
        int left = 0;
        int right = s.length - 1;

        while (left < right){
            swap(s, right, left);
            right --;
            left ++;
        }
    }

    void swap(char[] s, int right, int left){
        char temp = s[right];
        s[right] = s[left];
        s[left] = temp;
    }
}
```

Python

```python
class Solution:
    def reverseString(self, s: List[str]) -> None:
        left = 0
        right = len(s) - 1

        while (left < right):
            s[left], s[right] = s[right], s[left]
            left += 1
            right -= 1

```
