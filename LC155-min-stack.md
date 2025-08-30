# Question number and name
**Link**: [LeetCode Problem](https://leetcode.com/problems/min-stack)  
**Tags**: `Dual Stack`, `leetcode-medium`
## Intuition
Maintain two stacks: one for all values and one specifically for tracking minimum values. The minStack only stores values that are new minimums or equal to the current minimum, allowing O(1) access to the minimum value while preserving the stack structure.

## Walkthrough
1. **Initialisation**<br>
We need two separate stacks - one to store all pushed values in LIFO order, and another to specifically track the minimum values encountered so far.
```python
    def __init__(self):
        self.stack = []
        self.minStack = []
```
2. **Push Operation**<br>
Always add the value to the main stack. For the minStack, we only add the value if it's the first value, or if it's less than or equal to the current minimum. This ensures minStack always has the current minimum at the top while preserving previous minimums underneath.
```python
    def push(self, val: int) -> None:
        self.stack.append(val)
        if not self.minStack or self.minStack[-1] >= val:
            self.minStack.append(val)
```
3. **Pop operation**<br>
Remove the top value from the main stack. If the value being removed is equal to the current minimum (top of minStack), we must also remove it from minStack because this instance of the minimum value is no longer in the main stack.
```python
    def pop(self) -> None:
        current = self.stack.pop()
        if current == self.minStack[-1]:
            self.minStack.pop()
```
4. **Top operation**<br>
Simply return the top element of the main stack without modifying either stack.
```python
    def top(self) -> int:
        return self.stack[-1]
```
5. **Get minimum operation**<br>
The top of minStack always contains the current minimum value in the entire stack, allowing constant time access to the minimum value.
```python
    def getMin(self) -> int:
        return self.minStack[-1]
```


## Complexity Analysis 
| Metric  | Value | Explanation |  
|---------|-------|-------------|  
| **Time**  | O(1) | Pop, append and lookups all constant in stacks |  
| **Space** | O(n) | Both stacks may store up to n elements in worst-case (when values are pushed in descending order) |  

## Takeaways
- "Optimize time -> use extra space": Space-time tradeoff is fundamental
- "Stack ops are O(1)": Lists in Python have amortized O(1) append/pop
- Duplicate Handling is Crucial: ensures each pop of a min value has a corresponding minStack pop
- Synchronized Stacks: 
  - Not every push goes to minStack - only new minima or duplicates
  - Every minStack pop corresponds to a main stack pop of a min value
- could optimize further by storing (value, count) in minStack for duplicates
- Shadow data structure is a general pattern used in e.g. LRU cache with hashmap + linked list