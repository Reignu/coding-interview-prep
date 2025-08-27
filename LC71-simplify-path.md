# 71. Simplify Path
**Link**: [LeetCode Problem](https://leetcode.com/problems/simplify-path/description/)  
**Tags**: `Greedy`, `Stack`, `leetcode-medium`
## Intuition
Use a stack to add valid directories by preprocessing the input and formatting the output at the end

## Walkthrough
1. Initialise a stack to store final resulting path
 ```python
stack = []
 ```
2. Preprocess directories using split and only store it if non-empty or non `.`
```python
dirs = [d for d in path.split("/") if d != "" and d != "."]
```
3. Iterate through each directory name
- `..` indicates going back a directory so remove its parent directory if stack is non-empty (i.e. non-root directory)
```python
        for dir_name in dirs:
            if dir_name == "..":
                if stack:
                    stack.pop()
            else:
                stack.append(dir_name)
```
4. Format final output with `/` for root and each of the directories
```python     
        return "/" + "/".join(stack)
```

## Complexity Analysis 
| Metric  | Value | Explanation |  
|---------|-------|-------------|  
| **Time**  | O(n) | splitting, filtering, processing (append, pop) and join are all linear time operations in this case |  
| **Space** | O(n) | dirs for storing directories and stack for the final output both max size `n` |  

## Takeaways
- **Separation of concerns:** Handle output formattting separately at the end once final content has been established (like join instead of ifs within the logic)
- **Preprocessing/input sanitisation:** Filter the input (ie don’t add redundant inputs like '.' in this case and ""] using for loop and if statement in the initialisation
- **Defensive programming:** Append to the stack as the last step (ie else) once everything else taken care of, clear/unobstructed happy case
- **Stack LIFO Matches Directory Navigation:**
Join Once at the End is Efficient (building string incrementally would be O(n^2) due to immutability)