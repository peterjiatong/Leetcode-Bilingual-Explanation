# Valid Anagram / 有效的字母异位词

Leetcode: https://leetcode.com/problems/valid-anagram/description/

中文力扣： https://leetcode.cn/problems/valid-anagram/description/

## Solution: HashTable / 哈希表

The key point of this problem is how to compare the total frequency of letters appearing in two strings, `s` and `t`. 

When processing the first string `s`, record the total frequency of each letter, then when reading the second string `t`, check whether the letters appearing in `t` also exist in `s`, and determine whether the total frequency of these letters in `t` is higher than in `s`.

My initial approach was to use a dictionary to store letter frequencies. later, i think using an array of length 26 combined with ASCII values to record letter frequencies is also a good choice. i will not elaborate on this further here.

本题的重点是如何比较两个字符串`s`和`t`中出现的字母的频率之和。

在读取第一个字符串 `s`时，记录其中每个字母出现的频率之和，在读取第二个字符串`t`时，检查`t`中出现的字母是否在`s`中也有出现，并判断`t`中相同字母的频率之和是否高于`s`中对应字母的频率之和。

笔者在解题时，第一反应是使用字典来存储字母的频率统计。随后考虑到使用一个长度为26的数组，并结合ASCII码来记录字母的频率之和也是一个不错的选择。在这里不过多展开讨论。

Java

```java
class Solution {
    public boolean isAnagram(String s, String t) {
        Map<Character, Integer> mydict = new HashMap<>(); // you can also use a dict if you want here

        for (int i = 0; i < s.length(); i++){
            mydict.put(s.charAt(i), mydict.getOrDefault(s.charAt(i), 0) + 1);
        }

        for (int i = 0; i < t.length(); i++){
            if (mydict.get(t.charAt(i)) == null) return false;
            mydict.put(t.charAt(i), mydict.get(t.charAt(i)) - 1);
        }

        for (int i: mydict.values()){
            if (i != 0) return false;
        }

        return true;
    }
}
```

```
class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        # mydict = defaultdict(int) # 
        mydict = {}

        for i in s:
            mydict[i] = mydict.get(i, 0) + 1

        for i in t:
            if i not in mydict:
                return False
            mydict[i] -= 1

        for i in mydict.values():
            if i != 0:
                return False

        return True
```
