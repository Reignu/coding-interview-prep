# Question number and name
**Link**: [LeetCode Problem](https://leetcode.com/problems/word-pattern/?envType=problem-list-v2&envId=nj0ovbs3)<br>
**Tags**: `Hash Map`, `String`, `leetcode-easy`

## Intuition
Split the string and use a hash map to store the pattern as keys and words as values and vice versa

## Walkthrough
1. Split the string into words by default using spaces
```python
words = s.split()
```
3. Handle edge case as it is impossible for pattern to match string if their length is not the same
```python
if len(pattern) != len(words):
    return False
```
4. Initialise hash map with pattern char as the key and vice versa
```python
char_to_word = {}
word_to_char = {}
```
5. Process pattern character and word within input simultanously using zip
```python
for c,w in zip(pattern, words):
```
6. Check if key already exists and if the value matches (if return statement not met, add value to corresponding hash map)
```python
   if c in char_to_word and char_to_word[c] != w:
            return False
    else:
        char_to_word[c] = w

    if w in word_to_char and word_to_char[w] != c:
            return False
    else:
        word_to_char[w] = c
```
7. At this point we confirmed the pattern matches the string, and satisfy the problem.
```python
return True
```

## Complexity Analysis 
| Metric  | Value | Explanation |  
|---------|-------|-------------|  
| **Time**  | O(n) | One pass is needed through each hash map where n is the length of pattern/number of words |  
| **Space** | O(n) | Each hash map stores up to n number of elements |  

## Takeaways
- Initially attempted to use a single hash map, and retrieve keys but this would be O(n^2) time complexity
- Use two hash maps for bijection
- Remember to use zip to process two data structures in one loop
- only access value using index if needed, otherwise access value directly
