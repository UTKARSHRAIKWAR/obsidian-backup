> **Binary Search** is a _divide‑and‑conquer_ searching technique that repeatedly halves a sorted list to locate a target element.

- Works only on **sorted** collections.
    
- Reduces the search space from _n_ elements to at most comparisons.
    

---

## **⚙️ Prerequisites**

- The input array **must be in non‑decreasing order**.
    
- Two index pointers are required:
    

|   |   |
|---|---|
|Pointer|Meaning|
|**low**|Index of the current leftmost element under consideration|
|**high**|Index of the current rightmost element under consideration|

---

## **🔍 How Binary Search Works**

1. **Initialize** low = 1 (or 0 for zero‑based arrays) and high = n (last index).
    
2. **Compute the middle**:
    
3. **Compare** the key with the element at mid (A[mid]):
    
    - If key == A[mid] → **found**; return mid.
        
    - If key < A[mid] → the key lies in the **left half**; set high = mid - 1.
        
    - If key > A[mid] → the key lies in the **right half**; set low = mid + 1.
        
4. **Repeat** steps 2‑3 while low ≤ high.
    
5. If the loop ends (low > high) the key is **not present**; return a sentinel (e.g., -1).
    

---

## **📈 Example 1: Searching for** **42** **in a 1‑to‑15 List**

|   |   |   |   |   |   |   |
|---|---|---|---|---|---|---|
|Step|low|high|mid|A[mid]|Decision|New low/high|
|1|1|15|$8$|29|42 > 29 → right|low = 9|
|2|9|15|$12$|47|42 < 47 → left|high = 11|
|3|9|11|$10$|36|42 > 36 → right|low = 11|
|4|11|11|$11$|42|**found**|—|

- **Comparisons performed:** 4
    
- A linear search would need up to 11 comparisons in the worst case for this position.
    

---

## **📈 Example 2: Searching for** **12** **(present)**

|   |   |   |   |   |   |
|---|---|---|---|---|---|
|Step|low|high|mid|A[mid]|Decision|
|1|1|15|$8$|29|12 < 29 → left|
|2|1|7|$4$|12|**found**|

- **Comparisons performed:** 2
    

---

## **❌ Example 3: Searching for** **30** **(absent)**

|   |   |   |   |   |   |
|---|---|---|---|---|---|
|Step|low|high|mid|A[mid]|Decision|
|1|1|15|$8$|29|30 > 29 → right|
|2|9|15|$12$|47|30 < 47 → left|
|3|9|11|$10$|36|30 < 36 → left|
|4|9|9|$9$|31|30 < 31 → left|
|5|9|8|–|–|**low > high** → not found|

- Loop terminates when low exceeds high; the algorithm reports **failure**.
    

---

## **🔄 Iterative Algorithm (Pseudocode)**

1. low ← 1
    
2. high ← n
    
3. **while** low ≤ high **do**  
    a. mid ← ⌊(low + high) / 2⌋  
    b. **if** key = A[mid] **return** mid  
    c. **else if** key < A[mid] **then** high ← mid - 1  
    d. **else** low ← mid + 1
    
4. **return** -1 _(key not found)_
    

- The loop condition low ≤ high guarantees termination.
    

---

## **📊 Complexity Summary**

|   |   |   |
|---|---|---|
|Metric|Binary Search|Linear Search|
|**Time** (worst case)|||
|**Comparisons**|≤|Up to _n_|
|**Space**|(iterative)||
|**Precondition**|Sorted array|No ordering required|

- For the 15‑element example, binary search needed at most 4 comparisons versus up to 15 for linear search.
    

---

## **🧩 Key Takeaways**

- **Sorted order** is mandatory.
    
- The algorithm repeatedly **halves** the search interval using mid.
    
- It terminates when the key is found **or** when low surpasses high.
    
- Binary search offers **logarithmic** time, making it far faster than linear search for large datasets.## 🔍 Binary Search Overview
    

> **Binary search** is a divide‑and‑conquer algorithm that repeatedly halves a sorted list to locate a target element.

- Works only on **sorted arrays**.
    
- At each step it compares the target with the **middle element** (the _mid_).
    
- Based on the comparison, the search continues in either the **left** or **right** sub‑array.
    

## **📐 Calculating the Midpoint**

> The **mid index** is computed as mid = (low + high) // 2.

- If the sub‑array runs from index **1** to **7**, mid = (1 + 7) // 2 = 4.
    
- For the range **9** to **15**, mid = (9 + 15) // 2 = 12.
    
- Subsequent sub‑ranges are calculated similarly, e.g.:
    
    - **5–7** → mid = 6
        
    - **8–11** → mid = 10
        
    - **13–15** → mid = 14
        

## **🔢 Comparison Steps Example**

|   |   |   |   |   |
|---|---|---|---|---|
|Target|Step|Mid Index|Mid Value|Decision|
|429|1|8|29|target > 29 → go right (9‑15)|
|429|2|12|47|target > 47 → go right (13‑15)|
|429|3|14|55|target > 55 → go right (15‑15)|
|429|4|15|62|target > 62 → **not found**|

|   |   |
|---|---|
|Target|Steps to Find|
|47|2 (mid = 8 → 12)|
|14|3 (mid = 8 → 12 → 14)|
|29 (middle)|1|

- **Best case**: target equals the first mid → **1 comparison**.
    
- **Worst case**: target resides at a leaf node → **⌈log₂ n⌉ comparisons**.
    

## **📊 Complexity Analysis**

|   |   |   |
|---|---|---|
|Case|Time Complexity|Reason|
|**Best**|**O(1)**|Target is the first middle element.|
|**Worst**|**O(log n)**|Must traverse from root to leaf (height of the search tree).|
|**Average**|**O(log n)**|Expected number of comparisons over all possible targets approximates the tree height.|

- The **height of the binary‑search tree** equals ⌈log₂ n⌉.  
    Example: for 16 elements, log₂ 16 = 4 levels → at most 4 comparisons.
    

## **🛑 Unsuccessful Searches**

> When the target is **absent**, the algorithm proceeds until the sub‑array collapses (low > high).

- Searching for **65** (outside the list) follows the same halving steps until the interval is empty → **4 comparisons** (same as worst case).
    
- Targets that fall between existing values (e.g., between 55 and 62) also end after the interval shrinks to nothing.
    

## **📏 Average Case Calculation**

> The **average number of comparisons** is the sum of comparisons for each element divided by n.

1. Count comparisons for every possible target (including unsuccessful ones).
    
2. Add them together.
    
3. Divide by the total number of elements n.
    

Because the comparison count for each element follows the tree depth, the average simplifies to a value proportional to log₂ n, confirming the **average-case complexity O(log n)**.