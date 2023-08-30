```python
class Solution:
    def isValid(self, s: str) -> bool:
        bracketDict = {'(' : ')', '{': '}', '[': ']'}
        stack = []

        for bracket in s:
            if bracket in bracketDict:
                stack.append(bracket)
            elif not stack or bracket != bracketDict[stack.pop()]:
                return False

        return stack == []
```