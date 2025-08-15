# 13. Roman to integer
**Link**: [LeetCode Problem](https://leetcode.com/problems/roman-to-integer/)  
**Tags**: `Hash Table`, `String`, `leetcode-easy`
## Intuition
Use a hash map/dictionary and process the string accordingly (watch out for order)

## Walkthrough
1. Initialise the hash map with roman symbols as keys and corresponding integer values
```python
class Solution:
    def romanToInt(self, s: str) -> int:
        roman = { 'I': 1,'V': 5,'X': 10,'L': 50, 
        'C': 100, 'D': 500, 'M': 1000
        }
```
2. Initialise result variable to store the integer representation (outside of the loop to avoid accidental overwrites)
```python
        res = 0
```
3. Iterate through string characters checking the order
```python
        for i in range(len(s)):
```
4. Check if the index + 1 is within bounds (so we can perform comparison) and if the decreasing order is upheld
```python
            if i + 1 < len(s) and roman[s[i]] < roman[s[i + 1]]:
                res -= roman[s[i]]
            else:
                res += roman[s[i]]
```
5. Once loop is finished, return the final variable
```python
        return res
```

## Complexity Analysis 
| Metric  | Value | Explanation |  
|---------|-------|-------------|  
| **Time**  | O(1)  | The algorithm iterates through the string once (`O(n)`), but since Roman numerals are limited (max length ~15), it's effectively constant time. |  
| **Space** | O(1)  | The hash map stores only 7 symbols (fixed size), regardless of input. |  
## Takeaways
- Hash Map for Symbol-to-Value Mapping and O(1) lookups
- Handling Subtractive Notation (watch out for edge cases!)
- Practical O(1): Even if the theoretical time is O(n), bounded input makes it constant.
