# 57. Insert Interval
**Link**: [LeetCode Problem](https://leetcode.com/problems/insert-interval))  
**Tags**: `Greedy`, `Array`, `leetcode-medium`
## Intuition
Find where the new interval belongs, merge all overlapping intervals by expanding its boundaries, then insert the result while preserving order.

## Walkthrough
1. Initialise newStart and newEnd (optional) for ease of reference later in the code.
```python
newStart, newEnd = newInterval[0], newInterval[1]
```
2. Initialise result array (can also be done in place, but this is not a requirement for this problem).
   Initialise two pointers i and n to keep track of the current index and upper bound
```python
        res = []
        i, n = 0, len(intervals)
```
3. Add non-overlapping intervals before newInterval by checking if it is within bounds and whether the new start is higher than the current end (mergeable interval not reached).
```python
        while i < n and newStart > intervals[i][1]:
            res.append([intervals[i][0],intervals[i][1]])
            i += 1
```
4. Merge overlapping intervals by finding where the new end is lower or equal to the current start (i.e. the new interval is contained within and therefore can be merged)
   To maximise the merged interval and satisfy the problem, take the start as the minimum of both intervals, and the end as the maximum of both.
```python
        merged = newInterval
        while i < n and intervals[i][0] <= newEnd:
            merged[0] = min(intervals[i][0], newStart)
            merged[1] = max(intervals[i][1], newEnd)
            i += 1
        res.append(merged)
```
5. Add remaining intervals (this can be done through while loop or extend slice, these can be added safely as is since mergeable intervals have been deal with.
   And finally return result.
```python
      res.extend(intervals[i:])
      return res
```

## Complexity Analysis 
| Metric  | Value | Explanation |  
|---------|-------|-------------|  
| **Time**  | O(n) | Single pass through intervals |  
| **Space** | O(1) | If not including the output array |  

## Takeaways
- Three-phase approach: Add non-overlapping before, merge overlaps, add non-overlapping after (break it down into subproblems to make it easier to deal with)
- Greedy merging: Expand the new interval to absorb all overlapping intervals
- Single-pass efficiency despite multiple loops: Process each interval exactly once
