 9
 +-0+ **Definition:** _Divide and Conquer_ is an algorithmic design paradigm that solves a problem by recursively breaking it into **smaller subproblems of the same type**, solving each subproblem independently, and then **combining** those solutions to form the solution to the original problem.

### **🔎 Key Characteristics**

- **Recursive decomposition** – each subproblem is solved using the same strategy.
    
- **Homogeneity of subproblems** – subproblems must be _the same kind_ of problem as the original (e.g., sorting → sorting).
    
- **Combine step** – a well‑defined method to merge sub‑solutions into the final answer.
    
- **Base case** – a sufficiently small instance that can be solved directly.
    

### **📊 General Procedure (in tabular form)**

|   |   |   |
|---|---|---|
|Step|Action|When to apply|
|1️⃣|**Check size** of problem .|If $|
|2️⃣|**Divide** into subproblems .|When $|
|3️⃣|**Conquer** each recursively using the same strategy.|Applies to every subproblem.|
|4️⃣|**Combine** the results of into the solution for .|Must have a valid merging method.|

### **✅ When Divide & Conquer Works**

- The **subproblems are of the same type** as the original problem.
    
- There exists an **efficient combine** operation.
    
- The problem can be **recursively reduced** until a trivial base case is reached.
    

> **Guideline:** If breaking the task changes its nature (e.g., “organizing a workshop” → “sending invitations, designing posters”), the approach is **not** divide and conquer.

### **🛠️ Common Divide & Conquer Algorithms**

|   |   |   |
|---|---|---|
|Algorithm|Problem Type|Typical Subproblem Size|
|Binary Search|Searching in a sorted array||
|Merge Sort|Sorting|(two halves)|
|QuickSort|Sorting|Variable (average )|
|Strassen’s Matrix Multiplication|Matrix multiplication|(four sub‑matrices)|
|Finding Max/Min|Selection|(divide array)|
|Mergesort‑like recurrence|General|(where )|

### **📈 Analyzing Divide & Conquer Algorithms**

- Use **recurrence relations** to express the running time:  
    $  
    where
    
    - = number of subproblems,
        
    - = factor by which the problem size shrinks,
        
    - = cost of dividing and combining.
        
- Solving the recurrence (via the Master Theorem or expansion) yields the **time complexity**.
    

### **🧩 Relation to Other Strategies**

|   |   |   |
|---|---|---|
|Strategy|Core Idea|Typical Use Cases|
|**Dynamic Programming**|Overlapping subproblems, store solutions|Shortest paths, knapsack|
|**Backtracking**|Explore all possibilities, prune infeasible branches|N‑Queens, Sudoku|
|**Branch & Bound**|Prune suboptimal branches using bounds|Integer programming|
|**Divide & Conquer**|Recursively split into independent, same‑type subproblems|Sorting, searching, matrix multiplication|

### **📌 Practical Checklist for Applying Divide & Conquer**

1. Identify the **input size** of the problem.
    
2. Verify that a **smaller instance of the same problem** can be extracted.
    
3. Ensure there is a **clear combine step** (e.g., merging two sorted lists).
    
4. Define a **base case** that can be solved directly (often constant time).
    
5. Formulate the **recurrence** and analyze its complexity.