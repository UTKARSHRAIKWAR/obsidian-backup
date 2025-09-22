### **Time Complexity**

- Measures **how fast** an algorithm runs as input size `n` grows.
    
- Focus: **number of operations, not real time.**
    

**Types:**

- **Best Case (Ω)** → Minimum time
    
- **Worst Case (O)** → Maximum time (upper bound)
    
- **Average Case (Θ)** → Expected time
    

---

### **Common Complexities**

|Complexity|Meaning|Example|
|---|---|---|
|**O(1)**|Constant|Access array element|
|**O(log n)**|Logarithmic|Binary Search|
|**O(n)**|Linear|Linear Search|
|**O(n log n)**|Linearithmic|MergeSort|
|**O(n²)**|Quadratic|Bubble Sort|
|**O(n³)**|Cubic|Matrix Multiplication|
|**O(2ⁿ)**|Exponential|Recursive Fibonacci|
|**O(n!)**|Factorial|Traveling Salesman|

---

### **How to Calculate**

- Count loops/operations → drop constants & smaller terms.  
    Example:
    

`for(i=0; i<n; i++)   // n times   for(j=0; j<n; j++) // n times      O(1);`

⟹ `n * n = n² = O(n²)`

---

### **Space Complexity**

- Measures **memory usage** of an algorithm.
    
- Includes:
    
    - Input storage
        
    - Auxiliary variables
        
    - Recursion stack
        
- Example:
    
    - Recursive Fibonacci → O(n) (stack space)
        
    - Iterative Fibonacci → O(1)
        

---

### **Trade-off**

- Use more memory to save time.  
    Examples:
    
- Hashing → O(1) lookup (extra memory).
    
- DP → stores results to avoid recomputation.
    

---

✅ **Key Rule of Thumb:**

- `O(log n)` → Excellent
    
- `O(n log n)` → Good
    
- `O(n²)` → Acceptable for small `n`
    
- `O(2ⁿ)` or `O(n!)` → Impractical for large `n`