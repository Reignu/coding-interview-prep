# Question number and name
**Link**: [LeetCode Problem](https://leetcode.com/problems/basic-calculator)  
**Tags**: `Shunting-Yard`, `Stack`, `leetcode-hard`
## Intuition
The key insight is handling parentheses by tracking the current sign using a stack. When encountering (, we push the current sign onto the stack. When encountering ), we pop from the stack. This maintains the correct sign context for expressions within parentheses.

Shunting Yard algorithm is a method for parsing mathematical expressions specified in infix notation (e.g., `3 + 4`) and converting them into postfix notation (e.g., `3 4 +`) or Reverse Polish Notation (RPN). This algorithm is particularly useful because operations in postfix notation can be easily computed using a stack, allowing for efficient calculation of expressions.

## Walkthrough
1. **Initialisation**<br>
We need to track the overall result, build multi-digit numbers, maintain the current sign, and handle nested parentheses by storing sign contexts.
```python
class Solution:
    def calculate(self, s: str) -> int:
        ans = 0
        num = 0
        sign = 1
        stack = [sign] 
```
2. **Digit processing**<br>
When we encounter digits, we're building a number. Multiply the existing number by 10 and add the new digit to handle multi-digit numbers correctly.
```python
        for c in s:
            if c.isdigit():
                num = num * 10 + int(c)
```
3. **Opening parenthesis**<br>
A `(` means we're entering a new expression scope. We push the current sign onto the stack to preserve it, as any signs inside these parentheses should be relative to this context.
```python
            elif c == '(':
                stack.append(sign)
```
4. **Closing parenthesis**<br>
A `)` means we're exiting the current expression scope. We pop the stack to restore the previous sign context that existed before this parentheses block.
```python
            elif c == ')':
                stack.pop()
```
5. **Operator processing**<br>
Operators signal that we've completed reading a number. We apply the current sign to the number and add it to the total. Then we determine the new sign based on the operator and the current parentheses context (top of stack). Finally, we reset the number builder.
```python
            elif c == '+' or c == '-':
                ans += sign * num
                sign = (1 if c == '+' else -1) * stack[-1]
                num = 0
```
6. **Final calculation**<br>
After processing all characters, there might be one final number that hasn't been added to the total (if the expression doesn't end with an operator). We apply the current sign to this last number and return the complete result.
```python
        return ans + sign * num
```


## Complexity Analysis 
| Metric  | Value | Explanation |  
|---------|-------|-------------|  
| **Time**  | O(n) | Single pass through the string |  
| **Space** |  O(n) | Stack depth (worst-case for deeply nested parentheses) |  

## Takeaways
- Stack for context: Use stack to track sign changes across parentheses boundaries
- Deferred evaluation: Process numbers only when encountering operators or end of string
- Sign propagation: Multiply current operator sign with stack top to handle nested signs
- Edge handling: Remember to process the last number after the loop
