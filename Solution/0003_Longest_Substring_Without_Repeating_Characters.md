# [Longest Substring Without Repeating Characters](https://leetcode.com/problems/longest-substring-without-repeating-characters/)

## Solution

**Solution 1: Sliding Window Approach**

The solution utilizes a sliding window approach to find the length of the longest substring in a given string without any repeating characters. It maintains a dictionary/map to store the most recent index of each ASCII character encountered. The algorithm iterates through the string, updating the start pointer and dict values as it finds repeated characters. The maximum length of a non-repeating substring is continuously updated during the iteration. Finally, the algorithm returns the maximum length found.

O(n) time, O(1) space

### C++
```c++
class Solution
{
public:
    int lengthOfLongestSubstring(string s)
    {
        // Vector to hold the 128 ASCII characters (not 256 b/c no extended ASCII characters)
        // All elements are initialized to -1 instead of 0 so the 1st occurence of any char will set start = 0
        vector<int> dict(128, -1);
        
        // Initialize helper variables to track the start index and max substring length
        int maxLen = 0, start = 0;

        for (int end = 0; end < s.length(); ++end)
        {
            // Start pointer becomes max of current start and index of previous occurence of the character + 1
            // If it's the 1st occurence of the character, dict[s[i]] + 1 = -1 + 1 = 0
            start = max(start, dict[s[end]] + 1);

            // Update most recent index of the character
            dict[s[end]] = end;

            // Calculate max length
            maxLen = max(maxLen, end - start + 1);
        }
        
        // Return max length
        return maxLen;
    }
};
```

### Python
```python
class Solution:
    def lengthOfLongestSubstring(self, s: str) -> int:
        map = {}    # Create a map of symbols to their most recent index
        longestLength = 0

        # Traverse the string and use a sliding window to keep track of the substring
        l = 0
        for r in range(len(s)):
            # If s[r] has a duplicate in the range, shift the window to after the 1st occurrence
            if s[r] in map:
                l = max(map[s[r]], l)

            # Calculate the longest substring length and update the map
            longestLength = max(longestLength, r - l + 1)
            map[s[r]] = r + 1

        return longestLength
```
