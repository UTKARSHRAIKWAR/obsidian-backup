## Definition

- **Problem**: Given a collection of intervals, merge all overlapping intervals into one.
    
- Each interval is represented as `[start, end]`.
    
- Example:  
    Input → `[[1,3], [2,6], [8,10], [15,18]]`  
    Output → `[[1,6], [8,10], [15,18]]`
    

---

## Steps / Approach

1. **Sort intervals** by starting time.
    
2. Initialize `merged = []`.
    
3. Iterate over intervals:
    
    - If `merged` is empty **OR** current interval does not overlap with last merged interval → append it.
        
    - Else (overlap exists) → merge by updating the `end` = `max(last.end, current.end)`.
        

---

```java

function merge(intervals):
sort intervals by start
merged = []     
for interval in intervals:
	if merged is empty OR merged[-1].end < interval.start:         merged.append(interval)
	else: merged[-1].end=max(merged[-1].end,interval.end)     return merged
```

---

## Complexity

- **Sorting**: O(n log n)
    
- **Merge traversal**: O(n)
    
- **Total**: O(n log n)
    
- **Space**: O(n) (result storage)
    

---

## When to Use

- Scheduling problems (e.g., meeting rooms).
    
- Range merging in arrays.
    
- Calendar events.
    
- Overlapping tasks or intervals.
    

---
