# 150. Evaluate Reverse Polish Notation
**Link**: [LeetCode Problem](https://leetcode.com/problems/evaluate-reverse-polish-notation)  
**Tags**: `Stack`, `leetcode-medium`
## Intuition
- Use a stack for RPN evaluation since operands precede operators in reverse order.
- Process tokens left-to-right in one pass instead of complex nested loops.
- Leverage dictionary lookups for operations to avoid repetitive if-else statements.

## Walkthrough
1. Import the relevant libraries
```python
import operator
import math
```

2. **Stack Initialisation**<br>
Create an empty stack to store numeric values during evaluation.
```python
class Solution:
    def evalRPN(self, tokens: List[str]) -> int:
        stack = []
```
2. **Operations Mapping**<br>
Define a dictionary mapping operator symbols to their corresponding functions, with special handling for division to truncate toward zero.
```python
        ops = {
            '+': operator.add,
            '-': operator.sub,
            '*': operator.mul,
            '/': lambda a, b: math.trunc(a / b)  # Truncate towards zero
        }
```
3. **Token Iteration**<br>
Process each token in the input list sequentially from left to right.
```python     
        for token in tokens:
```

```python
            if token in ops:
```
```python
                b = stack.pop()
                a = stack.pop()
                result = ops[token](a, b)
                stack.append(result)
```
```python
            else:
                stack.append(int(token))
```
```python
        return stack[0]
```


## Complexity Analysis 
| Metric  | Value | Explanation |  
|---------|-------|-------------|  
| **Time**  | O(n) | Single pass through all tokens |  
| **Space** | O(n) | Worst-case stack stores all operands before operations |  

## Takeaways
- Use operator functions instead of if statements for cleaner code and avoid repetition
- Truncate division toward zero using math.trunc() via lambda functions
- Process tokens with a single for loop instead of nested while loops
- Store only operands in stack, not operators
- Use dictionary lookups for dynamic function execution with ops[token]
- Pop second operand first to maintain correct mathematical order
- Return stack[0] as final result since only one element remains