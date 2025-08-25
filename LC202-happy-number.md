# Question number and name
**Link**: [LeetCode Problem](<https://leetcode.com/problems/happy-number/>)  
**Tags**: `HashMap`, `HashSet`, `leetcode-easy`,`TOP150-list`

## Intuition
Repeatedly summing the squares of digits acts as a deterministic function that must eventually either converge to 1 (a fixed point) or enter a cycle, and we can detect this cycle efficiently with a hash set.

## Walkthrough
1. Define function to calculate the next number as sum of squares of its digits.<br>
   Convert to string to access individual digits, and convert back to perform calculation.
```
        def calculate_next(num):
            num = str(num)
            res = 0
            for n in num:
                res += int(n)**2
            return res
```
2. Initialise a set to keep track of unique numbers that have already been seen.
```
        seen = set()
```
3. Loop until happy number is found (signified by number 1).
```
        while n != 1:
```
4. If we encounter a result previously stored in a set, this means a loop and we are safe to return False.
```
            if n in seen:
                return False
```
5. If number is not seen before, we add it to the set and calculate n for the next iteration.
```
            seen.add(n)
            n = calculate_next(n)
```
6. If we get to the end of the loop, it is safe to assume that a happy number has been found and we can return true.
```
        return True
```



## Complexity Analysis 
| Metric  | Value | Explanation |  
|---------|-------|-------------|  
| **Time**  | O(logn)  | Each number n has logn digits |  
| **Space** |  O(logn) | Set that stores the digits encountered |  

## Takeaways
- Cycle detection is essential to prevent infinite loops in number transformation problems.
- Hashsets provide efficient O(1) lookups for checking previously encountered numbers.
- The sum-of-squares operation reduces numbers quickly, creating predictable behaviour patterns.
- All numbers eventually reach 1 or enter a known cycle.
- String conversion provides clean digit extraction, though mathematical methods are equally valid.
